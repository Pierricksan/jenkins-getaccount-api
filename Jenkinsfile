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
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build and Deploy') {
      when {
        anyOf {
          branch 'master'
          branch 'testBranch'
        }
      }
      steps {
        script {
          def config_file = 'env/master/config.json'
          if (env.BRANCH_NAME == 'testBranch') {
            config_file = 'env/testBranch/config.json.json'
          }

          def config = readJSON file: config_file
          def cloudhub_username = config.cloudhub.username
          def cloudhub_password = config.cloudhub.password
          def cloudhub_env = config.cloudhub.environment
          def cloudhub_app_name = config.cloudhub.appName

          withEnv(["username=${cloudhub_username}", "password=${cloudhub_password}", "environment=${cloudhub_env}", "appName=${cloudhub_app_name}"]) {
            sh "mvn clean install -DmuleDeploy -DmuleDeploy.username=${cloudhub_username} -DmuleDeploy.password=${cloudhub_password} -DmuleDeploy.env=${cloudhub_env} -DmuleDeploy.application=${cloudhub_app_name}"
          }
        }
      }
    }
  }
}