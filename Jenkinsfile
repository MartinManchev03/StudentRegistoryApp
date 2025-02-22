pipeline {
    agent any

    environment {
        NODE_VERSION = '16'  // Set the Node.js version you want to use
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Node.js') {
            steps {
                script {
                    bat "npm install -g n"
                    bat "n ${NODE_VERSION}"  // Set the Node.js version
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Build Server') {
            steps {
                bat 'nohup npm run start &'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm run test'
            }
        }
    }

    post {
        always {
            cleanWs()  // Clean up the workspace after the build
        }
    }
}
