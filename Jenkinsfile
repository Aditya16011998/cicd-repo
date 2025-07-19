pipeline {
  agent any

  tools {
    maven 'Maven3' // Replace with your Jenkins Maven tool name
  }

  environment {
    ANYPOINT_CREDENTIALS = credentials('anypoint-credentials') // Jenkins credential ID (username/password pair)
    ANYPOINT_ENV = 'TESTING'                 // Your CH2 environment
    BUSINESS_GROUP_ID = 'cf705657-5e45-4b04-9ae3-04b6871033ff'  // Your BG ID
    TARGET = 'privatespace-test'            // CH2 target (private space)
  }

  stages {
    stage('Build & Deploy to CloudHub 2.0') {
      steps {
        sh '''
          mvn clean deploy -DmuleDeploy \
          -Danypoint.username=$ANYPOINT_CREDENTIALS_USR \
          -Danypoint.password=$ANYPOINT_CREDENTIALS_PSW \
          -Danypoint.environment=$ANYPOINT_ENV \
          -Danypoint.businessGroupId=$BUSINESS_GROUP_ID \
          -Dtarget=$TARGET
        '''
      }
    }
  }
}
