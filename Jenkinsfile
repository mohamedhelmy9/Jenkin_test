pipeline {
    agent any

    stages {

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
                sh 'docker build -t node-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop node-app || true
                    docker rm node-app || true

                    docker run -d \
                      --name node-app \
                      -p 3000:3000 \
                      node-app:latest
                '''
            }
        }
    }
}
