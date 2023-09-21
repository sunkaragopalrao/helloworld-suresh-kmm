pipeline {
    agent {
        label 'maven'
    }
    environment {
        DOCKER_TAG = "v${env.BUILD_NUMBER}"
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
                script {                
                   withCredentials([string(credentialsId: 'FOSSA_API_KEY_NAME', variable: 'fossaApiKey')]) {
                     env['FOSSA_API_KEY'] = $fossaApiKey
                       sh 'fossa analyze'
                                       
                    }
                }
            }
        }
        
        
    }
} 
