pipeline {
    agent {
        node {
            label 'devops1'
        }
    }

    stages {
        stage('Build apps') {
            steps {
                sh 'npm install'
            }
        }
        stage('Testing') {
            steps {
                sh '''npm test
                    npm run test:coverage'''
            }
        }
        stage('Scanning Code') {
            steps {
                sh '''sonar-scanner   -Dsonar.projectKey=training-devops   -Dsonar.sources=.   -Dsonar.host.url=http://10.23.2.2:9000   -Dsonar.login=sqp_b6c238d0265878cd9b8da127a7be64c0f14bd138'''
            }
        }
        stage('Build Image') {
            steps {
                sh '''
                docker compose build
                '''
            }
        }
        stage('Deploy Apps') {
            steps {
                sh '''
                docker compose up -d
                '''
            }
        }
        stage('Push Image') {
            steps {
                sh ''' 
                docker compose push 
                '''
            }
        }
    }
}
