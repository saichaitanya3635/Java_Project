pipeline {
    
    agent {
                label 'ubuntu'
             }
    tools {
        maven {
                 installation: 'Maven 3.9.9', // The name of your Maven installation
        }
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
                
                script {
                    sh 'mvn clean install'
                }
            
          }
 }
}
}

        

       

    
