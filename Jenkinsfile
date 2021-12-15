pipeline {
	
	agent {label 'Windows-Agent-Astha'}

    stages {
        
        stage ('Clean workspace') {
          steps {
                  cleanWs()
                }
				}
	    stage ('Git Checkout') {
           steps {
                  git branch: 'master',url: 'https://github.com/asthagangwar3/jenkins-ci-template.git'
                 }
  }	
  
      
        stage('Restore-Packages') {	
		steps{
            bat 'C://Users//Administrator//Downloads//softwares//nuget.exe restore C://Users//Administrator//Desktop//jenkins-ci-template//src//MyWindowsService\MyWindowsService.sln'
		     }
			 }
			 
		stage('Build') {
		steps{
			bat 'msbuild C:\Users\Administrator\Desktop\jenkins-ci-template\src\MyWindowsService\MyWindowsService\Deploy-Windows-Service-Via-MSBuild.proj'
		 }
		}
		
		stage('Pre-Processing') {
		steps{
		    bat 'C:\Users\Administrator\Downloads\softwares\sonar-scanner\SonarQube.Scanner.MSBuild.exe begin /k:"Jenkins_CI_Dotnet" /d:sonar.host.url="http://3.234.193.237:9000/" /d:sonar.login="6c6431244ceb22769eb35e51c9b42e23c048c3f1"'
			}
		
		}
		
		stage('Rebuild'){
		steps{
		    bat '"C:\Program Files (x86)\MSBuild\14.0\Bin\amd64\MSBuild.exe" "C://Users//Administrator//Desktop//jenkins-ci-template//src//MyWindowsService//MyWindowsService.sln" /t:Rebuild'
			}
			}
			
		stage('Post-processing') {
		steps{
             bat 'C:\Users\Administrator\Downloads\softwares\sonar-scanner\SonarQube.Scanner.MSBuild.exe end /d:sonar.login="6c6431244ceb22769eb35e51c9b42e23c048c3f1" '
           }
		   }
           		
      
       
	} 
      
      
      }
    
