pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "7fceab2c-eb9d-457a-b64e-2f8a617db023"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
           sh 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          sh "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'sandbox-hellocicd-tcs'
        DEPLOY_CREDS = credentials('deploy-anypoint-user')
    	MULE_VERSION = '4.3.0'
    	BG = "7fceab2c-eb9d-457a-b64e-2f8a617db023"
    	WORKER = "Micro"
      }
      steps {
           /* sh 'mvn deploy -P cloudhub -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%"'*/
           sh 'mvn deploy -P cloudhub -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dapp.name="%APP_NAME%" -Danypoint.env="%ENVIRONMENT%"'
      }
    }
   /* stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = 'production-hellocicd-tcs'
        DEPLOY_CREDS = credentials('deploy-anypoint-user')
    	MULE_VERSION = '4.3.0'
    	BG = "7fceab2c-eb9d-457a-b64e-2f8a617db023"
    	WORKER = "Micro"
      }
      steps {
           sh 'mvn deploy -X -P cloudhub -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" '
      }
    }*/
  }

  tools {
    maven 'm3'
  }
}