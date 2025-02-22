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
                    sh "npm install -g n"
                    sh "n ${NODE_VERSION}"  // Set the Node.js version
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Build Server') {
            steps {
                sh 'nohup npm run start &'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm run test'
            }
        }
    }

    post {
        always {
            cleanWs()  // Clean up the workspace after the build
        }
    }
}
