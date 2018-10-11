pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean mvn-project-package'
            }
        }
    }
}
