
pipeline {
    agent any

    environment {
        GIT_BRANCH = 'main'
        GIT_URL = 'https://github.com/Guilene01/nodejs-app.git'
        NODE_VERSION = '14' // Specify the Node.js version you want to use
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control system (e.g., Git)
                git branch: "${GIT_BRANCH}", url: "${GIT_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }
        stage('Run ESLint') {
            steps {
                // Run ESLint for code linting
                sh 'npx eslint .'
            }
        }

        /*stage('Run Tests') {
            steps {
                // Run your tests (if any)
                sh 'npm test'
            }
        }

        stage('Build Application') {
            steps {
                // Build the application (if your app has a build step)
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (e.g., to a server or cloud service)
                echo 'Deploying the application...'
                // Add deployment commands here (e.g., scp, rsync, etc.)
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }*/
    }
}