pipeline {
    agent any
    environment {
        GIT_URL = 'git@github.com:berehx/jenkins.git' // SSH URL for GitHub
        BRANCH = 'main'  // Replace with your correct branch name
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/${env.BRANCH}"]], 
                          userRemoteConfigs: [[url: env.GIT_URL, credentialsId: 'your-ssh-key-id']]])
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
