pipeline {
    agent any

    environment{
        my_tag = "c:\\temp"
        //my_tag = my_tag
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