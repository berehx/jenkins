pipeline {
    agent any

    environment {
        REMOTE_HOST = 'user@remote-vm-ip'      // SSH login info for remote VM
        REMOTE_KEY = credentials('ssh-private-key') // SSH private key credential in Jenkins
    }

    stages {
        // Stage 1: Checkout from GitHub repository
        stage('Checkout') {
            steps {
                checkout scm  // This checks out the code from the Git repository
            }
        }

        // Stage 2: Build (Optional - if you need to compile or prepare the project)
        stage('Build') {
            steps {
                echo 'Building project...'
                // Add your build commands here if needed (e.g., Maven, Gradle, etc.)
            }
        }

        // Stage 3: Deploy to Remote VM (Install Apache server or deploy application)
        stage('Deploy') {
            steps {
                script {
                    sshagent([REMOTE_KEY]) {
                        // Install Apache (httpd) on the remote server (for example)
                        sh '''
                        ssh $REMOTE_HOST "sudo apt update"
                        ssh $REMOTE_HOST "sudo apt install -y apache2"
                        '''
                    }
                }
            }
        }

        // Stage 4: Verify Deployment (Check Apache status or application status)
        stage('Verify Deployment') {
            steps {
                script {
                    sshagent([REMOTE_KEY]) {
                        // Check if Apache is running on the remote server
                        sh 'ssh $REMOTE_HOST "systemctl status apache2"'
                    }
                }
            }
        }

        // Stage 5: Test Deployment (Optional - Check if the app works as expected)
        stage('Test') {
            steps {
                script {
                    sshagent([REMOTE_KEY]) {
                        // Test the deployment by checking if Apache responds on port 80
                        sh 'ssh $REMOTE_HOST "curl -I http://localhost"'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment pipeline executed successfully!'
        }
        failure {
            echo 'Deployment pipeline failed!'
        }
    }
}

