pipeline {
    agent any

    stages {
        // Stage 1: Build the project
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Use a build automation tool, e.g., Maven
                    sh 'mvn clean package'
                }
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example of running tests
                    sh 'mvn test'
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code for best practices...'
                    // Use a static analysis tool, e.g., SonarQube
                    sh 'sonar-scanner'
                }
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Use a security tool like OWASP ZAP
                    sh 'zap-cli quick-scan http://localhost:8080'
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                    // Deploy to staging server using AWS CLI, for example
                    sh 'aws s3 cp target/app.jar s3://my-staging-bucket/'
                }
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Example of running tests on a staging server
                    sh 'curl -X GET http://staging-server-url/tests'
                }
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production server...'
                    // Deploy to production server using AWS CLI or another tool
                    sh 'aws s3 cp target/app.jar s3://my-production-bucket/'
                }
            }
        }
    }

    // Email notifications after certain stages
    post {
        success {
            mail to: 's224755066@deakin.edu.au',
                 subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                 body: "The pipeline completed all stages successfully."
        }
        failure {
            mail to: 's224755066@deakin.edu.au',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline failed. Please check the logs for details."
        }
    }
}
