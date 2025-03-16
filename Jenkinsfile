
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'node:18' // Specify the Node.js Docker image you want to use
        GIT_BRANCH = 'main'
        GIT_URL = 'https://github.com/Guilene01/nodejs-app.git'
        
        
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your version control system (e.g., Git)
                git branch: "${GIT_BRANCH}", url: "${GIT_URL}"
            }
        }
        stage('Build and installDependencies') {
            steps {
                script {
                    // Run the Node.js container for building and testing
                    docker.image("${DOCKER_IMAGE}").inside('-u 995:991') {
                        sh 'npm ci'
                    }
                }
            }
        }
        /*stage('Run ESLint') {
            steps {
                script {
                // Run ESLint for code linting
                docker.image("${DOCKER_IMAGE}").inside('-u 995:991') {
                    sh 'npm install -g eslint'
                    sh 'eslint .'
                  }
                }
    
            }
        }
        stage('RunLint') {
            steps {
                script {
                // Run ESLint for code linting
                docker.image("${DOCKER_IMAGE}").inside('-u 995:991') {
                    sh 'npx standard'
                  }
                }
    
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