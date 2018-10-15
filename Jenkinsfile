pipeline {
    agent any
	tools {
        maven 'maven'
    }
    stages{
        stage('Build'){
            steps {
                bat 'npm install'
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
