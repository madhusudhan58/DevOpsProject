pipeline {

    agent any

    environment {

        IMAGE_NAME = "madhu58/devopsproject"
        IMAGE_TAG = "v1"

    }

    stages {

        stage('Checkout') {

            steps {

                checkout scm

            }

        }

        stage('Build Docker Image') {

            steps {

                bat 'docker build -t %IMAGE_NAME%:latest .'

            }

        }

        stage('Docker Login') {

            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    bat '''
                    docker logout
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    docker info
                    '''

                }

            }

        }

        stage('Tag Image') {

            steps {

                bat 'docker tag %IMAGE_NAME%:latest %IMAGE_NAME%:%IMAGE_TAG%'

            }

        }

        stage('Push Image') {

            steps {

                bat 'docker push %IMAGE_NAME%:%IMAGE_TAG%'

            }

        }

        stage('Pull Image Test') {

            steps {

                bat 'docker pull %IMAGE_NAME%:%IMAGE_TAG%'

            }

        }

        stage('Run Container') {

            steps {

                bat '''
                docker rm -f devopsapp || exit 0
                docker run -d --name devopsapp %IMAGE_NAME%:%IMAGE_TAG%
                '''

            }

        }

    }

    post {

        success {

            echo 'CI/CD Pipeline Completed Successfully'

        }

        failure {

            echo 'Pipeline Failed'

        }

    }

}