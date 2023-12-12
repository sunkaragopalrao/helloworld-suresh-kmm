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
        stage("Docker Build"){
            steps{
                sh label: '', script: '''docker build --build-arg JAR_FILE=target/*.jar .'''
            }
        }
        
        
    }
} 
