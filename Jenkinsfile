pipeline {
    agent any
	
	tools {
        maven 'maven'
    }
    stages{
        stage('Build'){
            steps{
                bat "mvn clean package"
				
				// -t is tag 
				bat "docker build . -t tomcatwebapp:${env.BUILD_ID}"
               
            }

        }
    }
}