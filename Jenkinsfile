pipeline {
  agent any
  stages {
    stage('Clean') {
      steps {
        sh 'echo "Clean"'
        sh 'cd stockpred'
        sh 'dotnet clean'
      }
    }

    stage('Checkout') {
      steps {
        sh 'echo "Hello World"'
      }
    }

    stage('Build') {
      steps {
        sh 'echo "Build"'
      }
    }

    stage('Test') {
      steps {
        sh 'echo "TEST"'
      }
    }

    stage('Release') {
      steps {
        sh 'echo "Release"'
      }
    }

    stage('Deploy') {
      steps {
        sh 'echo "Hello Deploy"'
      }
    }

  }
}