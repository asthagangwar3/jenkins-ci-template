pipeline {
	
	agent {label 'Windows-Agent-Astha'}
	
	environment { 
        SONAR_CREDS = credentials('Sonar_Token')		
        Branch = 'develop'
    }

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
            bat 'C://Users//Administrator//Downloads//softwares//nuget.exe restore C://Users//Administrator//Desktop//jenkins-ci-template//src//MyWindowsService//MyWindowsService.sln'
		     }
			 }
			 
		stage('Build') {
		steps{
			bat 'msbuild C://Users//Administrator//Desktop//jenkins-ci-template//src//MyWindowsService//MyWindowsService//Deploy-Windows-Service-Via-MSBuild.proj'
		 }
		}
		
		stage('Pre-Processing') {
		steps{
			  withSonarQubeEnv('Sonar')
			{
		    bat 'C://Users//Administrator//Downloads//softwares//sonar-scanner//SonarQube.Scanner.MSBuild.exe begin /k:Jenkins_CI_Dotnet'
			}
		}
		
		}
		
		stage('Rebuild'){
		steps{
		    bat '"C://Program Files (x86)//MSBuild//14.0//Bin//amd64//MSBuild.exe" "C://Users//Administrator//Desktop//jenkins-ci-template//src//MyWindowsService//MyWindowsService.sln" /t:Rebuild'
			}
			}
			
		stage('Post-processing') {
		steps{
			 withSonarQubeEnv('Sonar')
			{
             bat 'C://Users//Administrator//Downloads//softwares//sonar-scanner//SonarQube.Scanner.MSBuild.exe end'
           } 
		}
		   }
	    
	    stage('quality gate'){
	      steps{       
              waitForQualityGate abortPipeline: true 
                }
	      
             }   
           		
      
       
	} 
      
      
      }
