pipeline {
    agent any
	tools {
        maven 'maven'
        jdk 'javaJDK'
    }
    stages{
        stage('Build'){
            steps {
                sh 'npm install'
            }
			post {
				success{
					echo 'Now Archiving'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
        }
		stage ('Deploy to Staging'){
			steps {
				build job: 'deploy-to-staging'
			}
		}
    }
}
