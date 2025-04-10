pipeline {
    agent any

    environment {
        // Define the GitHub repository URL and the credentials ID for SSH key authentication
        GITHUB_REPO_URL = 'git@github.com:berehx/jenkins.git'
        GIT_CREDENTIALS_ID = 'your-ssh-key-id'  // Replace this with your actual credentialsId
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the repository using SSH with the specified credentials
                git credentialsId: "${GIT_CREDENTIALS_ID}", url: "${GITHUB_REPO_URL}"
            }
        }

        stage('Install Apache') {
            steps {
                // Example of installing Apache server (httpd) on the system
                script {
                    sh 'sudo apt update && sudo apt install -y apache2'
                }
            }
        }

        stage('Start Apache') {
            steps {
                // Start the Apache server
                script {
                    sh 'sudo systemctl start apache2'
                }
            }
        }

        stage('Check Apache Status') {
            steps {
                // Check if Apache is running
                script {
                    sh 'sudo systemctl status apache2'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Any additional deployment steps can go here
                echo 'Deployment completed.'
            }
        }
    }

    post {
        always {
            // Actions to be run after the pipeline, such as cleanup
            echo 'Pipeline completed'
        }
    }
}
