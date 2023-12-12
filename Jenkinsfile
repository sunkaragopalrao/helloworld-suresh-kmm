pipeline {
    agent any
    
    
    stages {
        
        stage("Build Project"){
            steps{
                sh label: '', script: '''mvn clean install'''

            }
        }
        stage("Unit Test"){
            steps{
                sh label: '', script: '''mvn test'''
            }
        }
        
        
    }
} 
