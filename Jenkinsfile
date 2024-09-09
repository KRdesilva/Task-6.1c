pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    bat 'mvn clean package'  // Use bat for Windows
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    bat 'mvn test'  // Use bat for Windows
                }
            }
        }

        // Add other stages with 'bat' instead of 'sh'
    }

    post {
        success {
            mail to: 'kavindyadesilva19@gmail.com',
                 subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                 body: "The pipeline completed all stages successfully."
        }
        failure {
            mail to: 'kavindyadesilva19@gmail.com',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline failed. Please check the logs for details."
        }
    }
}
