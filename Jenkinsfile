pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Running PowerShell script...'
                bat 'powershell -ExecutionPolicy Bypass -File script.ps1'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'recipient@example.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build succeeded! Check: ${env.BUILD_URL}"
            )
        }
        failure {
            emailext (
                to: 'recipient@example.com',
                subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed. Check: ${env.BUILD_URL}"
            )
        }
    }
}
