pipeline {
    agent any
    environment {
        JFROG_PLATFORM_URL = 'https://trialufqsz0.jfrog.io'
        DOCKER_IMAGE = 'my-springboot-app'
        ARTIFACTORY_REPO = 'docker-local'
        SERVER_ID = 'trialufqsz0'  // Set the correct server ID
    }
    tools {
        maven 'Maven 3.9.9'
        jfrog 'jfrog-cli'
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Configure JFrog CLI') {
            steps {
                withCredentials([string(credentialsId: 'JF_ACCESS_TOKEN', variable: 'JF_ACCESS_TOKEN')]) {
                    sh 'jfrog config add $SERVER_ID --url=$JFROG_PLATFORM_URL --access-token=$JF_ACCESS_TOKEN --interactive=false'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }
        stage('Push to JFrog Artifactory') {
            steps {
                sh '''
                jfrog rt docker-push $DOCKER_IMAGE:latest $ARTIFACTORY_REPO --server-id=$SERVER_ID
                '''
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop springboot-app || true
                docker rm springboot-app || true
                docker run -d --name springboot-app -p 8080:8080 --restart=always $JFROG_PLATFORM_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest
                '''
            }
        }
    }
}
