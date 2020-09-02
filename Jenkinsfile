pipeline {
    agent { label "master" }
    environment { 
        ECR_REGISTRY = "046402772087.dkr.ecr.us-east-1.amazonaws.com"
        APP_REPO_NAME= "callahan-repo/todo-app"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build --force-rm -t "$ECR_REGISTRY/$APP_REPO_NAME:latest" .'
                sh 'docker image ls'
            }
        }
        stage('Create ECR Repo') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 && docker login --username AWS --password-stdin "$ECR_REGISTRY"'
                sh 'aws ecr create-repository \
                        --repository-name "$APP_REPO_NAME" \
                        --image-scanning-configuration scanOnPush=false \
                        --region us-east-1'
                sh 'docker push "$ECR_REGISTRY/$APP_REPO_NAME:latest"'
            }
        }
    }
    post { 
        always { 
            echo 'Deleting all local images'
            sh 'docker image prune -af'
        }
    }
}