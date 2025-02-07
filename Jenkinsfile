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
                label 'WIN-TM'
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

        

       

    
