pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'maven clean mvn-project-package'
            }
        }
    }
}
