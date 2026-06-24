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
         bat 'python app.py'
      }
   }

   stage('Test') {
      steps {
         echo 'Testing Successful'
      }
   }

 }

}