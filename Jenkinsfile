pipeline {
    agent { label 'ubuntu' } // The agent is defined at the pipeline level

    tools {
        maven 'Maven 3.9.9' // Correct syntax for Maven tool installation
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs() // Clean workspace
                git 'https://github.com/saichaitanya3635/demo.git' // Clone repository
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install' // Run Maven build
                }
            }
        }
    }
}
