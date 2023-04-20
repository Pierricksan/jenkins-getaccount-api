pipeline {
  agent any
  tools{
      maven 'Maven 3.8.8'
      jdk 'openjdk-11'
  }
  triggers {
      pollSCM('H/1 * * * *')
  }
  stages {
    stage('Configuration Step') {
      steps {
        echo "Configuration en cours ... "
        script {
          config = readJSON file: "env/${env.BRANCH_NAME}/config.json"
          env = config.get("cloudhub")
        }
      }
    }
    stage('Build application') {
      steps{
        sh 'mvn clean install'
      }
    }
    stage ('Deploy application') {
      environment{
        ANYPOINT_CREDENTIALS = credentials ('PierrickunMulesoftPlatform')
      }
      steps {
        sh "mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -Denvironment=${env.environment} -DappName=${env.appName}"
      }
    }

  }
}