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
        stage('Publish'){
             steps{
               dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh 'dotnet publish WebApplication/WebApplication.csproj --configuration Release --no-restore'
               }
             }
        }
    stage('Deploy') {
       steps{
              dir('Jenkins-.NET-Core-CI-CD-pipeline-dev') {
               sh '''for pid in $(lsof -t -i:80); do
                       kill -9 $pid
               done'''
               sh 'cd WebApplication/bin/Release/netcoreapp3.1/publish/'
               sh 'nohup dotnet WebApplication.dll --urls="http://34.100.229.18:80" --ip="34.100.229.18" --port=80 --no-restore > /dev/null 2>&1 &'
                
            	script{
		    sshagent(credentials : ['stock-host-machine'], ignoreMissing: true) {    
			    sh  '''ssh -o StrictHostKeyChecking=no stock@34.100.229.18 ./home/sakthi_dhandapani/invoke.sh'''
		      }
		     }
             }
       }
    }

  }
}
