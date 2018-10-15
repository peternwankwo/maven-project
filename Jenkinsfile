pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo 'this is it'
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
