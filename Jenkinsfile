pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'c1fb8df4-6585-41ed-85ff-5805a589d5da'  // Replace with your Netlify Site ID
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')  // Replace with your Jenkins credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your repository
                checkout scm
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo "🔧 Checking required files..."
                sh '''
                    test -f index.html || (echo "Missing index.html" && exit 1)
                    test -f netlify/functions/app.js || (echo "Missing script function" && exit 1)
                    echo "Build check passed."
                '''
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
                echo "Hello page load..."
                sh '''
                    npm install uuid
                    node -e "require('./netlify/functions/app.js'); console.log('Script function loaded successfully')"
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo "Deploying to Netlify..."
                // Install Netlify CLI and deploy the project
                sh '''
                    npm install netlify-cli
                    npx netlify deploy \
                      --auth=$NETLIFY_AUTH_TOKEN \
                      --site=$NETLIFY_SITE_ID \
                      --dir=. \
                      --prod
                '''
            }
        }

        stage('Post Deploy') {
            steps {
                echo "Deployment complete! Hello Page."
            }
        }
    }

    post {
        success {
            echo "CI/CD pipeline finished successfully."
        }
        failure {
            echo "Pipeline failed. Check logs for details."
        }
    }
}