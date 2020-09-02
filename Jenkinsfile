pipeline {
    agent docker
    environment { 
        ECR_REGISTRY = "046402772087.dkr.ecr.us-east-1.amazonaws.com"
        APP_REPO_NAME= "callahan-repo/todo-app"
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t "$ECR_REGISTRY/$APP_REPO_NAME:latest" .'
                sh 'docker image ls'
                sh 'docker rmi "$ECR_REGISTRY/$APP_REPO_NAME:latest"'
                sh 'docker image ls'
            }
        }
    }
}