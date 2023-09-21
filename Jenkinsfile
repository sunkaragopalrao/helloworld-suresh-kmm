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
                                
                   withCredentials([string(credentialsId: 'FOSSA_API_KEY_NAME', variable: 'fossaApiKey')]) {
                     //sh 'env[\'FOSSA_API_KEY\'] = $fossaApiKey'
                   // sh 'curl -H \'Cache-Control: no-cache\' https://raw.githubusercontent.com/fossas/fossa-cli/master/install-latest.sh | bash'
                       sh 'fossa analyze --fossa-api-key=$fossaApiKey'
                                       
                }
            }
        }
        
        
    }
} 
