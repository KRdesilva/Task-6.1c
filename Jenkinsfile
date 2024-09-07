pipeline {
    agent any
    environment {
        EMAIL_RECIPIENT = 's224755066@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean package'  // Replace with your build command
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'  // Replace with your test command
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                sh 'sonar-scanner'  // Replace with your SonarQube command
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'zap-cli quick-scan http://your-staging-url'  // Replace with your security scan command
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name MyDeploymentGroup --revision location=s3://mybucket/myapp.zip'  // Replace with your deployment command
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'selenium-server -role hub'  // Replace with your integration test command
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name MyDeploymentGroup --revision location=s3://mybucket/myapp.zip'  // Replace with your production deployment command
            }
        }
    }
    post {
        always {
            echo 'Sending email notifications...'
            emailext (
                to: "${EMAIL_RECIPIENT}",
                subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME}' (${env.BUILD_NUMBER})",
                body: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME}' (${env.BUILD_NUMBER})\n\n" +
                      "See console output at: ${env.BUILD_URL}",
                attachmentsPattern: '**/target/*.log'  // Adjust as needed
            )
        }
    }
}
