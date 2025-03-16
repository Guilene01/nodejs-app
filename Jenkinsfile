pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'node:18' // Specify the Node.js Docker image you want to use
        GIT_BRANCH = 'main'
        GIT_URL = 'https://github.com/Guilene01/nodejs-app.git'
        SONAQUBE_CRED = 'sonarqube-cred'
        SONAQUBE_INSTALLATION = 'sonar'
        APP_NAME = 'nodejs-app'
        SCANNER_HOME = tool 'sonar-env'
        SONARQUBE_IMAGE = 'sonarsource/sonar-scanner-cli:latest'
        CONTENTFUL_SPACE_ID = credentials('contentful-space-id')
        CONTENTFUL_ACCESS_TOKEN = credentials('contentful-access-token')
        CONTENTFUL_ENVIRONMENT = 'master'
        
    }

    stages {
        stage('Checkout') {
            steps {
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

                        // Add "type": "module" to package.json
                        sh 'npm pkg set type=module'

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
                        sh 'npx eslint . --max-warnings 0 --fix'
                    }
                }
            }
        }
        stage('SonarQube Scan') {
            steps {
                script {
                    docker.image("${SONARQUBE_IMAGE}").inside('-u root') {
                        withSonarQubeEnv(credentialsId: "${SONAQUBE_CRED}", installationName: "${SONAQUBE_INSTALLATION}") {
                            sh '''
                            sonar-scanner \
                                -Dsonar.projectName=${APP_NAME} \
                                -Dsonar.projectKey=${APP_NAME} \
                                -Dsonar.sources=. \
                                -Dsonar.java.binaries=.    
                            '''
                        }
                    }
                }
            }
        }
        stage('Run Unit Tests') {
    steps {
        script {
            docker.image("${DOCKER_IMAGE}").inside('-u root') {
                sh 'npm test -- --coverage'
            }
        }
    }
     }
      stage('Publish Test Results') {
            steps {
                junit '**/test-results.xml' // Adjust the path to match your test results file
            }
        }
    }
}