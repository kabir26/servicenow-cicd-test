pipeline {
  agent any
  environment {
    APPSYSID = '5d28b5d52f34701057c3ad6df699b6d1'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS_DEV = '7f071fc8-c7dc-42c8-85f2-89dd81bd051a'
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
        snPublishApp(credentialsId: "${CREDENTIALS_DEV}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
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
