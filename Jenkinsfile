pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'ls -ltr'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
                sh 'npm run build'
                sh 'ls -ltr'
            }
        }
        stage('Test') {
            steps {
                sh 'ls -ltr'
                sh 'grep index.html /build/index.html'
                npm run test
            }
        }
    }
}
