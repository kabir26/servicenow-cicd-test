pipeline {
  agent any
  environment {
    APPSYSID = '5d28b5d52f34701057c3ad6df699b6d1'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS_DEV = '8b58be0f-7c0b-4fa6-b420-4e6fe87c35d0'
    CREDENTIALS_PROD = 'a321eae6-8738-4828-94bb-6f12a70585c4'
    DEVENV = 'https://dev86082.service-now.com/'
    PRODENV = 'https://dev92566.service-now.com/'
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS_DEV}")
      }
    }
    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS_PROD}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
