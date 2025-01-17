pipeline {
    agent any
    environment{
        NETLIFY_SITE_ID 'c0abb5a8-2301-4f0a-b355-2947e7d25bfa'
    }

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
        stage('Test') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true 
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            
            }
        }
           stage('deploy') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true 
                }
            }
            steps {
                sh '''
                   npm install netlify-cli 
                   node_modules/.bin/netlify --version
                   echo "deploying to production: $NETLIFY_SITE_ID"
                '''
            }
        }
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
