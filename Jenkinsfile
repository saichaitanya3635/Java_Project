pipeline {
    agent any
    environment {
        ARTIFACTORY_URL = 'trialufqsz0.jfrog.io'
        DOCKER_IMAGE = 'my-springboot-app'
        ARTIFACTORY_REPO = 'docker-local'
    }
    tools {
        maven 'Maven 3.9.9'
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
        stage('Authenticate Docker with JFrog') {
            steps {
                withCredentials([string(credentialsId: 'JF_ACCESS_TOKEN', variable: 'JFROG_ACCESS_TOKEN')]) {
                    sh "echo '${JFROG_ACCESS_TOKEN}' | docker login $ARTIFACTORY_URL -u 'ACCESS-TOKEN' --password-stdin"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $ARTIFACTORY_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest .'
            }
        }
        stage('Push to JFrog Artifactory') {
            steps {
                sh 'docker push $ARTIFACTORY_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest'
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop springboot-app || true
                docker rm springboot-app || true
                docker run -d --name springboot-app -p 8080:8080 --restart=always $ARTIFACTORY_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest
                '''
            }
        }
    }
}
