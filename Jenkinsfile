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
    }
}

        

       

    
