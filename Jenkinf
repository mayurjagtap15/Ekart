pipeline {
    agent any
    
    tools {
        jdk 'jdk'
        maven 'maven3'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
              git branch: 'main', credentialsId: '7570db03-3269-40b5-9632-8c6903772630', url: 'https://github.com/mayurjagtap15/Ekart.git'
            }
        }
        
        stage('Compile') {
            steps {
                script {
                    sh "mvn clean compile -DskipTests=true"
                }
            }
        }
        
       stage('Build') {
            steps {
                script {
                    sh "mvn clean package -DskipTests=true"
                }
            }
       }  
       
         stage('Docker Build Image') {
            steps {
                script {
                 withDockerRegistry(credentialsId: '7a9c816a-3eb9-4d16-9dcf-facb932277e6', toolName: 'docker') {
                     sh "docker build -t shopping-kart -f docker/Dockerfile ."
                     sh "docker tag shopping-kart mayurjagtap15/shopping-kart:latest"
                     sh "docker push mayurjagtap15/shopping-kart:latest"
                    }   
                    
                }
            }
        }
        
      
        
      
    }
}
