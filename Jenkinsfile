pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/mohamedhelmy9/Jenkin_test.git'
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop my-app || true
                    docker rm my-app || true

                    docker run -d \
                      --name my-app \
                      -p 3000:3000 \
                      my-app:latest
                '''
            }
        }
    }
}
