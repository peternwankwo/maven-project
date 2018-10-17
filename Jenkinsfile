pipeline {
    agent any
		
    parameters {
         string(name: 'tomcat_dev', defaultValue: 'ec2-13-59-142-199.us-east-2.compute.amazonaws.com', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'ec2-18-191-109-243.us-east-2.compute.amazonaws.com', description: 'Production Server')
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
		
		stage ("SCA: ChekStyle"){
		    steps {
			echo 'Hello, Checkstyle'
		    }
		}
		
		stage ("SCA: SonarQube"){
		    steps {
			echo 'Hello, Sonar'
		    }
		}
		
		stage ("SCA: Fortify"){
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
                    steps {
                        bat "scp -v -o StrictHostKeyChecking=no -i D:/tomcat/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}