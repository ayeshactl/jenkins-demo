pipeline {
    agent any

    environment {
        APP_NAME = "maven-app"
        IMAGE_NAME = "maven-app-image"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning Git repository...'
                git url: 'https://github.com/YOUR_USERNAME/jenkins-demo.git', branch: 'main'
            }
        }

        stage('Build Maven Project') {
            steps {
                echo 'Building Maven project...'
                sh 'mvn clean package'
            }
        }

        stage('Check Target Jar') {
            steps {
                echo 'Verifying build output...'
                sh 'ls -l target/'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                sh '''
                    docker stop $APP_NAME || true
                    docker rm $APP_NAME || true
                    docker run -d --name $APP_NAME -p 8080:8080 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline SUCCESS — App is running!'
        }
        failure {
            echo '❌ Pipeline FAILED — check logs'
        }
    }
}
