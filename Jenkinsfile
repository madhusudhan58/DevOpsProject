pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Python') {
            steps {
                bat '''
                "C:\\Users\\Lenovo\\AppData\\Local\\Python\\pythoncore-3.14-64\\python.exe" --version
                '''
            }
        }

        stage('Build') {
            steps {
                bat '''
                "C:\\Users\\Lenovo\\AppData\\Local\\Python\\pythoncore-3.14-64\\python.exe" app.py
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Build Successful'
            }
        }
    }
}