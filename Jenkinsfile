pipeline {
    agent any
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
        
        
        
    }
} 
