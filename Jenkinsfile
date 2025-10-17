pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('humeradoc')
        IMAGE_NAME = "humeradoc/zomato_app"
        IMAGE_TAG = "v1"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/angelhumera/zomato_app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post {
        success {
            echo "🎉 Docker image pushed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
