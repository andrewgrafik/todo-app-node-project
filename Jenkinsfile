pipeline {
    agent { label "master" }
    stages {
        
        stage('Build Docker Image') {
            steps {
                sh 'docker --version'
                sh 'aws --version'
            }
        }
        stage('Create ECR Repo') {
            steps {
                sh 'git --version'
            }
        }
        
    }
    
}