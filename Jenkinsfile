pipeline {
  agent any

  tools {
    maven 'Maven3' // 👈 this should match the name from Global Tool Configuration
  }

  environment {
    ANYPOINT_CREDENTIALS = credentials('anypoint-credentials')
    ANYPOINT_ENV = 'TESTING'
    WORKER_TYPE = 'Micro'
  }

  stages {
    stage('Build & Deploy to CloudHub') {
      steps {
        sh '''
          mvn clean deploy -DmuleDeploy \
          -Danypoint.username=$ANYPOINT_CREDENTIALS_USR \
          -Danypoint.password=$ANYPOINT_CREDENTIALS_PSW \
          -Danypoint.environment=$ANYPOINT_ENV \
          -Dworker.type=$WORKER_TYPE
        '''
      }
    }
  }
}
