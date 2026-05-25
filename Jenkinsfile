pipeline {
    agent any

    stages {

        stage('Checkout') {
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
                sh 'docker build -t maven-app-image .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop maven-app || true
                docker rm maven-app || true
                docker run -d --name maven-app -p 80:8080 maven-app-image
                '''
            }
        }
    }

    post {
        success {
            echo "✅ SUCCESS"
        }
        failure {
            echo "❌ FAILED"
        }
    }
}
