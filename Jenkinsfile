pipeline {

    agent any

    environment {

        IMAGE = 'madhu58/devopsproject'

    }

    stages {

        stage('Checkout') {

            steps {

                checkout scm

            }

        }

        stage('Build Docker Image') {

            steps {

                bat 'docker build -t %IMAGE% .'

            }

        }

        stage('Docker Login') {

            steps {

                withCredentials([usernamePassword(

                credentialsId: 'dockerhub',

                usernameVariable: 'USER',

                passwordVariable: 'PASS'

                )]) {

                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'

                }

            }

        }

        stage('Tag Image') {

            steps {

                bat 'docker tag %IMAGE%:latest %IMAGE%:v1'

            }

        }

        stage('Push Image') {

            steps {

                bat 'docker push %IMAGE%:v1'

            }

        }

    }

}