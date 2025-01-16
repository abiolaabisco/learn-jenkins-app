pipeline {
    agent any

    stages {
        stage('build without docker') {
            steps {
                sh '''
                    ls -ltra
                    echo "Hello World from Abiola without docker"
                    touch containar-no.txt
                '''
            }
        }
        stage('build with docker') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true 
                }
            }
            steps {
                sh '''
                    ls -ltra
                    npm --version
                    node --version
                    echo "build with docker"
                    npm ci
                    npm run build
                    ls -ltra
                '''
            }
        }
        stage('test') {
            steps {
                sh 'test -f /build/index.html'
            
            }
        }
    }
}
