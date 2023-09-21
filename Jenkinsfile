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
                    //def shell = pipelineUtilities.getShellCommand()


                    //pre-scan setup - just clone. Fossa doesn't need build tool setup.
                    //pipelineUtilities.cleanWorkspaceAndCheckoutSourceCode(pconfig)

                    withCredentials([string(credentialsId: 'FOSSA_API_KEY_NAME', variable: 'fossaApiKey')]) {
                        env['FOSSA_API_KEY'] = fossaApiKey

                        "${shell}"("fossa list-targets")

                    "${shell}"("fossa analyze" +
                            " --title " + test-project +
                            
                            " --release-group-release '1.0' " +
                            " --debug")
                    }

                    
                }
            }
        }
        
        
    }
} 
