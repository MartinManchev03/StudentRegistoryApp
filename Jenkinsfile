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
                    // Install project dependencies
                    sh 'npm ci'
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
