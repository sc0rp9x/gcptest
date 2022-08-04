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

     stage('Deploy'){
	    
             steps{
		
		sshagent(credentials : ['stock-host-machine'], ignoreMissing: true) {
		dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
		
		sh 'sudo nginx -s reload'
		sh 'sudo systemctl restart nginx'
		sh 'sudo systemctl stop stockpred.service'
		sh 'sudo systemctl start stockpred.service'
               sh '''ssh -o StrictHostKeyChecking=no sakthi_dhandapani@34.100.229.18 '''
	       sh 'scp -r WebApplication/bin/Release/netcoreapp3.1/* sakthi_dhandapani@34.100.229.18:/var/www/html/stockpred'
             }
	     }
	     }
    }
	
  }
}
