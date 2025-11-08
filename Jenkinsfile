pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/VarshikaAnand/aws-cicd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'

            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                
            }
        }
    }
}
