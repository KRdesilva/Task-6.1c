pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/path/to/code'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'production'
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching source code from directory: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo "Waiting for manual approval"
                sleep 10
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}
