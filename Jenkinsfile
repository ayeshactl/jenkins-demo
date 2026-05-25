pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ayeshactl/jenkins-demo.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t maven-app-image .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop maven-app || true
                docker rm maven-app || true
                docker run -d -p 8081:8080 --name maven-app maven-app-image
                '''
            }
        }
    }
}
