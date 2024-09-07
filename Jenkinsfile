pipeline {
    agent any
    environment {
        // Set your email configuration here
        EMAIL_RECIPIENT = 'kavindyadesilva19@gmail.com'
        EMAIL_SUBJECT = "Build #${env.BUILD_NUMBER} - ${currentBuild.result}"
        EMAIL_BODY = """\
        Build result: ${currentBuild.result}
        
        Job Name: ${env.JOB_NAME}
        Build Number: ${env.BUILD_NUMBER}
        Build URL: ${env.BUILD_URL}
        """
    }
    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the source code from Git
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh './your-build-script.sh'
                    } else {
                        bat 'your-build-script.bat'
                    }
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running Unit and Integration Tests...'
                    // Add your test commands here
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Running Code Analysis...'
                    // Add your code analysis commands here
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Running Security Scan...'
                    // Add your security scan commands here
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to Staging...'
                    // Add your deployment commands here
                }
            }
        }
    }
    post {
        always {
            script {
                emailext (
                    to: "${EMAIL_RECIPIENT}",
                    subject: "${EMAIL_SUBJECT}",
                    body: "${EMAIL_BODY}"
                )
            }
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
