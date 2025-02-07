pipeline {
    agent any
    tools {
        maven 'Maven-3.9.9'  // Use the installed Maven from Jenkins
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-springboot-app .'
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop springboot-app || true
                docker rm springboot-app || true
                docker run -d --name springboot-app -p 8080:8080 --restart=always my-springboot-app
                '''
            }
        }
        stage('Verify') {
            steps {
                sh 'curl -s http://127.0.0.1:8080/welcome || exit 1'
            }
        }
    }
}
