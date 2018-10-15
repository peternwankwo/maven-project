pipeline {
    agent any
	tools {
        maven 'Maven 3.5.4'
        jdk 'jdk8'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
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
