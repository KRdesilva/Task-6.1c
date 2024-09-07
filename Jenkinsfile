pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit tests with JavaUnit...'
                echo "Running integration tests with Selenium..."
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code quality with SonarQube...'
                    // Add your code analysis commands here
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities with SAST scanner...'
                // Add your security scan commands here
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging server using AWS...'
            }
        }

        stage('IntegrationTests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production server using AWS tools...'
            }
        }
    }

    post {
        success {
            mail to: "s224755066@deakin.edu.au",
                subject: "Pipeline success - Build # ${currentBuild.number}",
                body: "The pipeline has successfully completed all steps. Build logs are attached."
        }

        failure {
            mail to: "s224755066@deakin.edu.au",
                subject: "Pipeline failure - Build # ${currentBuild.number}",
                body: "The pipeline has failed at stage ${currentBuild.currentResult}. Build logs are attached."
        }
    }
}
