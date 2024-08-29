pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean install' // Example build step using Maven for Windows
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                bat 'mvn test' // Run unit and integration tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                bat 'sonar-scanner' // Run SonarQube analysis for Windows
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for security vulnerabilities...'
                bat 'dependency-check.bat --project JenkinsPipeline --scan .' // OWASP Dependency-Check for Windows
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'aws s3 cp target/my-app.jar s3://my-staging-bucket/' // Example deployment step for AWS S3 on Windows
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on Staging...'
                // Integration tests logic
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'aws s3 cp target/my-app.jar s3://my-production-bucket/' // Example deployment step for AWS S3 on Windows
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            deleteDir() // Clean up workspace
        }
        success {
            mail to: 'developer@example.com',
                 subject: "Pipeline Success: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Build successful: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'developer@example.com',
                 subject: "Pipeline Failed: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Build failed: ${env.BUILD_URL}"
        }
    }
}
