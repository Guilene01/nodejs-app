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

        stage('Build and Install Dependencies') {
            steps {
                script {
                    // Run the Node.js container for building and testing
                    docker.image("${DOCKER_IMAGE}").inside('-u root') {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Setup ESLint') {
            steps {
                script {
                    // Install ESLint and create a configuration file
                    docker.image("${DOCKER_IMAGE}").inside('-u root') {
                        // Install the latest ESLint version
                        sh 'npm install eslint@latest --save-dev'

                        // Create a basic ESLint configuration file (eslint.config.js)
                        sh '''
                            echo "export default [
                              {
                                languageOptions: {
                                  ecmaVersion: 'latest',
                                  sourceType: 'module'
                                },
                                rules: {
                                  indent: ['error', 2],
                                  quotes: ['error', 'single'],
                                  semi: ['error', 'always']
                                }
                              }
                            ];" > eslint.config.js
                        '''
                    }
                }
            }
        }

        stage('Run ESLint') {
            steps {
                script {
                    // Run ESLint for code linting
                    docker.image("${DOCKER_IMAGE}").inside('-u root') {
                        sh 'npx eslint . --max-warnings 0'
                    }
                }
            }
        }
    }
}