pipeline {
    agent any

    environment {
<<<<<<< HEAD
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

=======
        NETLIFY_SITE_ID = 'c1fb8df4-6585-41ed-85ff-5805a589d5da'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
<<<<<<< HEAD
                echo "🔧 Checking required files..."
                sh '''
                    test -f index.html || (echo "❌ Missing index.html" && exit 1)
                    test -f netlify/functions/app.js || (echo "❌ Missing script function" && exit 1)
                    echo "✅ Build check passed."
=======
                echo "Checking required files..."
                sh '''
                    test -f public/index.html || (echo "Missing public/index.html" && exit 1)
                    echo "Build check passed."
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
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
<<<<<<< HEAD
                echo "Hello page load..."
                sh '''
                    npm install uuid
                    node -e "require('./netlify/functions/app.js'); console.log('✅ Script function loaded successfully')"
=======
                echo "Testing quote function load..."
                sh '''
                    node -e "require('./netlify/functions/quote.js'); console.log('Function loaded successfully')"
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
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
<<<<<<< HEAD
                echo "🚀 Deploying to Netlify..."
                // Install Netlify CLI and deploy the project
=======
                echo "Deploying to Netlify..."
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
                sh '''
                    npm install netlify-cli
                    npx netlify deploy \
                      --auth=$NETLIFY_AUTH_TOKEN \
                      --site=$NETLIFY_SITE_ID \
<<<<<<< HEAD
                      --dir=. \
=======
                      --dir=public \
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
                      --prod
                '''
            }
        }

        stage('Post Deploy') {
            steps {
<<<<<<< HEAD
                echo "✅ Deployment complete! Hello Page."
=======
                echo "Deployment complete! Your app is live."
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
            }
        }
    }

    post {
        success {
<<<<<<< HEAD
            echo "🎉 CI/CD pipeline finished successfully."
        }
        failure {
            echo "❌ Pipeline failed. Check logs for details."
=======
            echo "CI/CD pipeline finished successfully."
        }
        failure {
            echo "Pipeline failed. Check logs for details."
>>>>>>> bcb335f87298d093348ba764bfc7d9e27a911cdb
        }
    }
}