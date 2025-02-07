pipeline {
    agent any
    stages {
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
