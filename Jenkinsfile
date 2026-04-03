pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'a37f6db4-29b2-4b08-a9fa-102cf7e935e0'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Netlify...'
                sh 'npm install -g netlify-cli'
                sh 'netlify deploy --prod --dir=build --site=$NETLIFY_SITE_ID --auth=$NETLIFY_AUTH_TOKEN'
            }
        }
    }
}