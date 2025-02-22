pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Setup Node.js
                    sh "npm install -g n"
                    sh "n ${NODE_VERSION}"

                    // Install project dependencies
                    sh 'npm ci'
                }
            }
        }

        stage('Build Server') {
            steps {
                sh 'npm run start &'
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
            cleanWs()
        }
    }
}
