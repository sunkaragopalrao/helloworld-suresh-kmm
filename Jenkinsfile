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
                sh label: '', script: '''
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 863532638265.dkr.ecr.us-east-1.amazonaws.com
                docker build --build-arg JAR_FILE=target/*.jar -t java-app .'''
            }
        }
        stage("push Image"){
            steps{
                sh label: '', script: '''
                docker tag java-app:latest 863532638265.dkr.ecr.us-east-1.amazonaws.com/java-app:latest
                docker push 863532638265.dkr.ecr.us-east-1.amazonaws.com/java-app:latest'''
            }
            
        }        
        
    }
} 
