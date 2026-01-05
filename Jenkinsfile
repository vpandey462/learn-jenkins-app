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
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'ls -ltr'
                sh 'test -f build/index.html'
                sh 'npm run test'
            }
        }
    }
    post {
        always {
            junit 'test-result/junit.xml'
        }
    }
}
