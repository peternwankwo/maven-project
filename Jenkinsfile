pipeline {
    agent any
		
    parameters {
         string(name: 'tomcat_dev', defaultValue: 'ec2-18-220-255-166.us-east-2.compute.amazonaws.com', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'ec2-18-218-1-94.us-east-2.compute.amazonaws.com', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                bat "mvn clean package"
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
        stage ('Test'){
			parallel{
				stage ('Unit test'){
					steps {
					echo 'Hello, Unit test'
					}
				}

				stage ("Functional test"){
					steps {
					echo 'Hello, Integration Test'
					}
				}
				
				stage ("SonarQube"){
					steps {
					echo 'Hello, Sonar'
					}
				}
				
				stage ("Fortify"){
					steps {
					echo 'Hello, Fortify'
					}
				}
			}
        }
 
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Stagging'){
                    steps {
						bat "scp -v -o StrictHostKeyChecking=no -i D:/tomcat/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }
 
                stage ("Deploy to Production"){
				
					//to do.....
					// add restriction to group that can deploy to Production
					//Add conditions i.e protractor, unit tests pass, SonarQube
			
					steps{
						timeout(time:5, unit:'DAYS'){
							input message:'Approve PRODUCTION Deployment?'
						}

						bat "scp -v -o StrictHostKeyChecking=no -i D:/tomcat/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
					}
					post {
						success {
							echo 'Code deployed to Production.'
						}

						failure {
							echo ' Deployment failed.'
						}
					}
					
									
                }
            }
        }
    }
}