pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
         sh 'rm -rf gcptest'
         git branch: '$BRANCH_NAME', credentialsId:'stock-user-2022', url:'https://github.com/sc0rp9x/gcptest.git'
      }
    }
  stage('Clean') {
      steps {
        sh 'echo "Clean"'
        
        cd /var/lib/jenkins/workspace/gcptest_main/stockpred
        
        sh pwd
        sh 'dotnet clean'
      }
    }
    stage('Build') {
      steps {
        sh 'echo "Build"'
        sh 'cd stockpred'
        sh 'dotnet build'
      }
    }

    stage('Test') {
      steps {
        sh 'echo "TEST"'
        sh 'cd stockpred'
        sh 'dotnet test'
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
