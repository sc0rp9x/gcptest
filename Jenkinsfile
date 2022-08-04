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
             dir('stockpred') {
               sh 'dotnet restore stockpred.sln'
             }
            }
    }        
    stage('Clean'){
           steps{
             dir('stockpred') {
               sh 'dotnet clean stockpred.sln --configuration Release'
             }
            }
    } 

    stage('Build'){
           steps{
             dir('stockpred') {
               sh 'dotnet build stockpred.sln --configuration Release --no-restore'
             }
            }             
    }

     stage('Deploy'){
	    
             steps{
		
		sshagent(credentials : ['stock-host-machine'], ignoreMissing: true) {
		dir('stockpred') {
               sh '''ssh -o StrictHostKeyChecking=no sakthi_dhandapani@34.100.229.18 '''
	       sh 'scp -r stockpred/bin/Release/netcoreapp3.1/* sakthi_dhandapani@34.100.229.18:/var/www/html/stockpred/'
             }
	     }
	     }
    }
	
  }
}
