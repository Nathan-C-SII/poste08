pipeline {
    agent any

    environment {
        APP_NAME = 'my-app'
        DOCKER_USER = 'nathansii'
    }

    stages {

        stage('Login Docker') {
            steps {
                withCredentials([string(
                    credentialsId: 'poste-08_DOCKER_PASSWORD',
                    variable: 'poste-08_DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    def buildVersion = "1.0.${env.BUILD_NUMBER}"
                    echo "Building ${APP_NAME} version ${buildVersion}"
                }
            }
        }

        stage('Test') {
            steps {
                echo "Testing ${APP_NAME}..."
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def buildVersion = "1.0.${env.BUILD_NUMBER}"
                    echo "Deploying ${APP_NAME} version ${buildVersion}"
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout || true'
        }
    }
}
