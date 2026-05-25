pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning Git repository...'
git branch: 'main', url: 'https://github.com/ayeshactl/jenkins-demo.git'            }
        }

        stage('Build Maven Project') {
            steps {
                echo 'Building Maven project...'
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t maven-app-image .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'

                sh '''
                docker stop maven-app || true
                docker rm maven-app || true
                docker run -d --name maven-app -p 8081:8080 maven-app-image
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline SUCCESS'
        }
        failure {
            echo '❌ Pipeline FAILED'
        }
    }
}
