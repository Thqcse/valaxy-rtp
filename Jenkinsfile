def imageName = 'stalin.jfrog.io/default-docker-local/valaxy-rtp'
def registry  = 'https://stalin.jfrog.io'
def version   = '1.0.3'
def app
pipeline {
    agent {
       node {
         label "valaxy"
      }
    }
    stages {
        stage('Build') {
            steps {
                echo '<--------------- Building --------------->'
                sh 'printenv'
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo '<------------- Build completed --------------->'
            }
        }
    
     stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'sonarqubescanner'
            }
            steps {
                echo '<--------------- Sonar Analysis Started --------------->'
                withSonarQubeEnv('sonarqube'){
                    sh "${scannerHome}/bin/sonar-scanner"
                }    
                echo '<--------------- Sonar Analysis Ends --------------->'
            }    
        }
    }
}
