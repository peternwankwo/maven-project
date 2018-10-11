pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                git 'https://github.com/peternwankwo/maven-project'
                sh 'mvn clean package'
            }
        }
    }
}
