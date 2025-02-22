pipeline {
    agent any

    environment {
        NODE_VERSION = '16.14.0'  // Set the Node.js version you want to use
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
                    if (isUnix()) {
                        sh "npm install -g n"
                        sh "n ${NODE_VERSION}"  // Set the Node.js version
                    } else {
                        bat "nvm install ${NODE_VERSION}"
                        bat "nvm use ${NODE_VERSION}"
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm ci'
                    } else {
                        bat 'npm ci'
                    }
                }
            }
        }

        stage('Build Server') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'nohup npm run start &'
                    } else {
                        bat 'start npm run start'
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm run test'
                    } else {
                        bat 'npm run test'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()  // Clean up the workspace after the build
        }
    }
}
