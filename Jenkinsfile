pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/VijayDabkara155/react-docker-21aug25.git'
            }
        }

        stage('Build React App') {
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
                // Stop old container (if running) and run new one
                sh '''
                docker rm -f react-docker-container || true
                docker run -d -p 80:80 --name react-docker-container react-docker-app
                '''
            }
        }
    }
}
