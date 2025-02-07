pipeline {
    agent {
                label 'ubuntu'
             }
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
                label 'ubuntu'
             }
            steps {
                // Build the project using Maven
                 tools {
                        maven 'Maven 3.9.9' // Replace 'Maven 3.8.6' with the name of your Maven installation
                 }
                script {
                    sh 'mvn clean install'
                }
            }
        }
    }
}

        

       

    
