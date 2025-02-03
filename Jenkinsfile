pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/saichaitanya3635/demo.git'
            }
        }

        stage('Build') {
            steps {
                // Build the project using Maven
                script {
                    sh 'mvn clean install'
                }
            }
        }

        

       

    post {
        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed. Please check the logs.'
        }

        always {
            cleanWs()  // Clean the workspace after build
        }
    }
}
