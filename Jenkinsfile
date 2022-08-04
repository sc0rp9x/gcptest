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

    stage('Build'){
           steps{
             dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh 'dotnet build WebApplication.sln --configuration Release --no-restore'
             }
            }             
    }
    stage('Test: Unit Test'){
           steps {
             dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
                sh 'dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore'
             }
            }
    }
     stage('Deploy'){
	    
             steps{
		
		sshagent(credentials : ['stock-host-machine'], ignoreMissing: true) {
		dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh '''ssh -o StrictHostKeyChecking=no sakthi_dhandapani@34.100.229.18 '''
	       sh 'pwd'
	       sh 'ls'
	       sh 'scp $WORKSPACE/bin sakthi_dhandapani@34.100.229.18:/jenkins/'
             }
	     }
	     }
    }
	
  }
}
