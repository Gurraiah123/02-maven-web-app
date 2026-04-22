pipeline {
    agent any

    environment {
        IMAGE_NAME = "ashokit-html-app"
        CONTAINER_NAME = "ashokit-container"
        PORT = "8080"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Gurraiah123/02-maven-web-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d \
                -p $PORT:80 \
                --name $CONTAINER_NAME \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully 🚀"
        }
        failure {
            echo "Deployment failed ❌"
        }
    }
}
