pipeline {
    agent any
    environment {
        ARTIFACTORY_URL = 'https://trialufqsz0.jfrog.io'
        DOCKER_IMAGE = 'my-springboot-app'
        ARTIFACTORY_REPO = 'docker-local'
    }
    tools {
        maven 'Maven 3.9.9'
    }
    stages {
        stage('Configure JFrog CLI') {
            steps {
                withCredentials([string(credentialsId: 'JF_ACCESS_TOKEN', variable: 'JF_ACCESS_TOKEN')]) {
                    sh 'jf c add trialufqsz0 --url=$ARTIFACTORY_URL --access-token=$JF_ACCESS_TOKEN --interactive=false'
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
                sh 'docker build -t $ARTIFACTORY_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest .'
            }
        }
        stage('Push to JFrog Artifactory') {
            steps {
                sh 'jf docker push $ARTIFACTORY_URL/$ARTIFACTORY_REPO/$DOCKER_IMAGE:latest'
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
