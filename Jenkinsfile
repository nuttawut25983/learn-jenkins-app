pipeline {
    agent any

    envarioment {
        NETLIFY_SITE_ID = 'a79da4a1-8d0b-45cd-a790-997ff5d0c793'
    }
    
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            
            steps {
                echo 'Testing...'
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('Deploy'){
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                echo 'Deploying...'
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploy To Production site ID: ${NETLIFY_SITE_ID}"
                '''
                }
            }
        }
    }
}
