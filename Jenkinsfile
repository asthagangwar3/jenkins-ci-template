pipeline {
	
	agent {label 'Windows-Agent-Astha'}

    stages {
        
        stage ('Clean workspace') {
          steps {
                  cleanWs()
                }
      
        stage('Build') {	
             
		     }
      
       
	} 
      stage('Sonar Analysis'){
        steps{
           
            withSonarQubeEnv('Sonar')
              {
                bat 'sonar-scanner'
              }
            }
             
        
            
         post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
           
                always {
               emailext body: 'A Test EMail',  to: '$DEFAULT_RECIPIENTS', subject: 'Test'
                }
            }
			}
       //stage('quality gate'){
	 //      steps{
           //     timeout(time: 1, unit: 'HOURS') {
             //   waitForQualityGate abortPipeline: true 
               // }
	      // }
             //}         
          
        } 
      
      
    }
