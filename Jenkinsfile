pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mafid456/Food-Delivery-forking.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    dir('backend') {
                        sh 'docker build -t my-backend:latest .'
                    }
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    dir('frontend') {
                        sh 'docker build -t my-frontend:latest .'
                    }
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    // Stop old containers if running
                    sh 'docker rm -f backend || true'
                    sh 'docker rm -f frontend || true'

                    // Start backend
                    sh 'docker run -d --name backend -p 5000:5000 my-backend:latest'

                    // Start frontend
                    sh 'docker run -d --name frontend -p 80:80 my-frontend:latest'
                }
            }
        }
    }
}
