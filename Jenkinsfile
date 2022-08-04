pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
         sh 'rm -rf gcptest'
         git branch: '$BRANCH_NAME', credentialsId:'stock-user-2022', url:'https://github.com/sc0rp9x/gcptest.git'
      }
    }
    stage('Build') {
     steps {
       sh 'pwd'
        dir('stockpred') {
          sh 'pwd'
         sh 'sudo dotnet build  /var/lib/jenkins/workspace/gcptest_main/stockpred'
         sh 'sudo dotnet build'
      }
      }
    }

    stage('Test') {
      steps {
        sh 'echo "TEST"'
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
