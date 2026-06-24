pipeline {

    agent any

    stages {

        stage('Git Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat '"C:\\Users\\Lenovo\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Build Successful'
            }
        }
    }
}