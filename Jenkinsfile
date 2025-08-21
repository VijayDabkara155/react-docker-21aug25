pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/VijayDabkara155/react-docker-21aug25.git'
            }
        }

        stage('Build React App') {
            agent {
                docker {
                    image 'node:18'   // ✅ Runs inside Node.js container
                }
            }
            steps {
                dir('my-app') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('my-app') {
                    sh 'docker build -t react-docker-app .'
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:80 --name react-container --restart unless-stopped react-docker-app || true'
            }
        }
    }
}
