pipeline {
    agent any
    tools{
        maven 'Maven 3.8.8'
        jdk 'openjdk-11'
    }
    stages {
        stage('Deploy') {
            steps {
                // sh 'apt-get install -y maven'
                sh 'mvn clean deploy -DmuleDeploy'
            }
        }
    }
}