pipeline {
    agent any

    environment {
        // Define environment variables if necessary
        EMAIL_RECIPIENT = 's224755066@deakin.edu.au'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example using Maven. Replace with your build tool if needed.
                    sh 'mvn clean install'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example using Maven. Replace with your test tool if needed.
                    sh 'mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    // Example using SonarQube. Replace with your code analysis tool if needed.
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Example using OWASP Dependency-Check. Replace with your security scan tool if needed.
                    sh 'dependency-check --project MyProject --scan .'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging...'
                    // Replace with your deployment script
                    sh './deploy-to-staging.sh'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Replace with your integration test script
                    sh './integration-tests.sh'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Replace with your deployment script
                    sh './deploy-to-production.sh'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded.'
            // Send success email
            emailext (
                to: "${env.EMAIL_RECIPIENT}",
                subject: "Pipeline Succeeded",
                body: "The pipeline has successfully completed.",
                attachmentsPattern: '**/test-results/*.xml'
            )
        }

        failure {
            echo 'Pipeline failed.'
            // Send failure email
            emailext (
                to: "${env.EMAIL_RECIPIENT}",
                subject: "Pipeline Failed",
                body: "The pipeline has failed. Please check the logs.",
                attachmentsPattern: '**/test-results/*.xml'
            )
        }
    }
}
