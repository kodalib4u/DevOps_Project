pipeline {
    agent {
        node {
           label "maven" 
        }
       
    }
    environment{
        PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
    }
    stages 
    {
        stage('Build Code') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('Test code') {
            steps {
                echo ".........Unit Test Started......."
                sh 'mvn surefire-report:report'
                echo ".........Unit Test completed......"
            }
        }
       
        stage("Quality Gate")
        {
               environment {
	            scannerHome = tool 'kodalib4u-sonarqube-scanner'
                        }
            steps
            {
             
             script
             {
               withSonarQubeEnv('sonarqube-server')
               timeout(time: 1, unit: 'HOURS') 
               { // Just in case something goes wrong, pipeline will be killed after a timeout
                 def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                 if (qg.status != 'OK') 
                 {
                   error "Pipeline aborted due to quality gate failure: ${qg.status}"
                 }
               }
             }
           }
        }
    }
}

