pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean install' // Example build step using Maven
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test' // Run unit and integration tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                sh 'sonar-scanner' // Run SonarQube analysis
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for security vulnerabilities...'
                sh 'dependency-check.sh --project JenkinsPipeline --scan .' // OWASP Dependency-Check
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'aws s3 cp target/my-app.jar s3://my-staging-bucket/' // Example deployment step to AWS S3
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on Staging...'
                // Assuming integration tests are run as part of deployment script
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'aws s3 cp target/my-app.jar s3://my-production-bucket/' // Example deployment step to AWS S3
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            deleteDir() // clean up workspace
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
