pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean pipeline-as-code'
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
