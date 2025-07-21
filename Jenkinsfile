pipeline {
  agent any

  tools {
    maven 'Maven3' // Match the Maven tool name in Jenkins
  }

  environment /*{
    ANYPOINT_CREDENTIALS = credentials('anypoint-credentials') // Username/password pair
    ANYPOINT_ENV = 'TESTING'
    BUSINESS_GROUP_ID = 'cf705657-5e45-4b04-9ae3-04b6871033ff'
    TARGET = 'privatespace-test'
    GROUP_ID = 'cf705657-5e45-4b04-9ae3-04b6871033ff'
    ARTIFACT_ID = 'git-cicd-test-app'
    VERSION = '1.0.0'
    ORG_ID = 'cf705657-5e45-4b04-9ae3-04b6871033ff'
  } */


  {
    ANYPOINT_CREDENTIALS = credentials('anypoint-credentials') // Username/password pair
    ANYPOINT_ENV = 'shubham-non-prod-env'
    BUSINESS_GROUP_ID = '709e9757-80fb-489c-8baf-2c6e1461c92c'
    TARGET = 'shubham-non-prod-env'
    GROUP_ID = '709e9757-80fb-489c-8baf-2c6e1461c92c'
    ARTIFACT_ID = 'git-cicd-test-app'
    VERSION = '1.0.0'
    ORG_ID = '709e9757-80fb-489c-8baf-2c6e1461c92c'
  }

  stages {

    stage('Build & Publish to Exchange') {
      steps {
        sh '''
          mvn clean deploy -DskipTests \
            -Danypoint.username=$ANYPOINT_CREDENTIALS_USR \
            -Danypoint.password=$ANYPOINT_CREDENTIALS_PSW \
            -Danypoint.organizationId=$ORG_ID
        '''
      }
    }

    stage('Deploy to CloudHub 2.0') {
      steps {
        sh '''
          mvn mule:deploy -DmuleDeploy \
            -Danypoint.username=$ANYPOINT_CREDENTIALS_USR \
            -Danypoint.password=$ANYPOINT_CREDENTIALS_PSW \
            -Danypoint.environment=$ANYPOINT_ENV \
            -Danypoint.businessGroupId=$BUSINESS_GROUP_ID \
            -Dtarget=$TARGET \
            -DgroupId=$GROUP_ID \
            -DartifactId=$ARTIFACT_ID \
            -Dversion=$VERSION
        '''
      }
    }

  }
}
