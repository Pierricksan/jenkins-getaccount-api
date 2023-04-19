pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                // sh 'apt-get install -y maven'
                sh 'mvn clean deploy -DmuleDeploy'
            }
        }
    }
}