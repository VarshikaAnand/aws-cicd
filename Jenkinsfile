pipeline {
    agent any
    environment {
        AWS_REGION = 'ap-south-1'
        IMAGE_NAME = 'aws-cicd-demo'
        ECR_REPO =  '443730190586.dkr.ecr.ap-south-1.amazonaws.com/aws-cicd-demo'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/VarshikaAnand/aws-cicd.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'echo "Building project..."'
               
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                docker tag $IMAGE_NAME:latest $ECR_REPO:latest
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                docker push $ECR_REPO:latest
                '''
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                docker stop $IMAGE_NAME || true
                docker rm $IMAGE_NAME || true
                docker pull $ECR_REPO:latest
                docker run -d -p 80:3000 --name $IMAGE_NAME $ECR_REPO:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Build/Deployment Failed.'
        }
    }
}
