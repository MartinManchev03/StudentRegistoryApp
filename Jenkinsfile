pipeline {
    agent any

    environment {
        NODE_VERSIONS = ['18.x', '20.x', '22.x']
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            matrix {
                axes {
                    axis {
                        name 'NODE_VERSION'
                        values '18.x', '20.x', '22.x'
                    }
                }
                stages {
                    stage('Setup Node.js') {
                        steps {
                            script {
                                sh "npm install -g n"
                                sh "n ${NODE_VERSION}"
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
                            sh 'npm run start &'
                        }
                    }

                    stage('Run Tests') {
                        steps {
                            sh 'npm run test'
                        }
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
