pipeline {
    agent any

    stages {
/*
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
*/
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
        
        stage('E2E Test') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.43.1-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                   npm install serve
                   npm modules/.bin/serve -s build &
                   sleep 10
                   npx playwright test
                '''
            }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
