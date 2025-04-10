pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the code from GitHub repository
                git 'https://github.com/berehx/jenkins.git'
            }
        }

        stage('Install Apache') {
            steps {
                script {
                    // You can install Apache directly without using sudo if Jenkins has the necessary permissions
                    sh 'apt-get update && apt-get install -y apache2'
                }
            }
        }

        stage('Start Apache') {
            steps {
                script {
                    // Start Apache service directly
                    sh 'systemctl start apache2'
                }
            }
        }

        stage('Check Apache Status') {
            steps {
                script {
                    // Check Apache service status
                    sh 'systemctl status apache2'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            // Actions that are always executed after the pipeline run (e.g., cleanup)
            echo 'Pipeline execution finished.'
        }
    }
}
