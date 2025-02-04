pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                cleanWs() 
                git 'https://github.com/saichaitanya3635/demo.git'
            }
        }

        stage('Build') {
            agent {
                label 'PMS-HPT'
             }
            steps {
                // Build the project using Maven
                script {
                    bat 'mvn clean install'
                }
            }
        }
    }
}

        

       

    
