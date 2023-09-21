pipeline {
    agent {
        label 'maven'
    }
    environment {
        DOCKER_TAG = "v${env.BUILD_NUMBER}"
        FOSSA_API_KEY = ""
    }
    options{
        // Stop the build early in case of compile or test failures
        skipStagesAfterUnstable()
    }
    stages {
        
        stage("Build Project"){
            steps{
                sh label: '', script: '''mvn clean install'''

            }
        }
        stage('SCA - Fossa Pilot - Scan') {
                    
            steps {
                              
                   withCredentials([string(credentialsId: 'FOSSA_API_KEY_NAME', variable: 'fossaApiKey')]) {
                       "${shell}"("fossa list-targets")
                       sh 'fossa analyze --fossa-api-key $fossaApiKey --title=test-mavne --debug'
                                       
                    
                }
            }
        }
        
        
    }
} 
