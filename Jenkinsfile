pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/ayeshactl/jenkins-demo.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t app-image .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop app-container || true
                docker rm app-container || true
                docker run -d --name app-container -p 80:8080 app-image
                '''
            }
        }
    }
}pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/ayeshactl/jenkins-demo.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t app-image .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop app-container || true
                docker rm app-container || true
                docker run -d --name app-container -p 80:8080 app-image
                '''
            }
        }
    }
}
