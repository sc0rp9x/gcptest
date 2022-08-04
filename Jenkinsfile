pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
         sh 'rm -rf gcptest'
         git branch: '$BRANCH_NAME', credentialsId:'stock-user-2022', url:'https://github.com/sc0rp9x/gcptest.git'
      }
    }
    stage('Restore packages'){
           steps{
             dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh 'dotnet restore WebApplication.sln'
             }
            }
         }        
        stage('Clean'){
           steps{
             dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh 'dotnet clean WebApplication.sln --configuration Release'
             }
            }
         }
  
    
    stage('Build') {
     steps {
       sh 'pwd'
        dir('stockpred') {
          dotnetBuild
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
