pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'maven clean package'
				echo "hahahaha"
            }
			post {
				success {
					echo 'Now archiving...'
					
				}
			
			}
        }
        stage('Deploy to staging') {
			/* agent section could go here as well */
            steps {
                echo 'Deploying....'
            }
        }
    }
}