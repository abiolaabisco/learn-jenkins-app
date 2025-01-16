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
                    echo "build with docker"
                    touch container-yes.txt
                '''
            }
        }
    }
}
