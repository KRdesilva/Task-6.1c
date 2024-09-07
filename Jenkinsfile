pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'nohup ./your-build-script.sh &'
                    } else {
                        // Run the batch file, ensure it exists and is correctly referenced
                        bat 'your-build-script.bat'
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Add your test commands here
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Add your code analysis commands here
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Add your security scan commands here
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Add your deployment commands here
            }
        }
    }
}
