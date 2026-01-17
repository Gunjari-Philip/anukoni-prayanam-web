pipeline {
    agent any

    environment {
        IMAGE_NAME = "novel-blog"
        CONTAINER_NAME = "novel-blog-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning repository"
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f ${CONTAINER_NAME} || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name ${CONTAINER_NAME} -p 8080:80 ${IMAGE_NAME}:latest'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Pipeline Failed!"
        }
    }
}



