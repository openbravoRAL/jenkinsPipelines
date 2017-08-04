pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stage ("Setup") {
    def workspace = pwd()
    echo workspace

    def isBuildNumber = workspace.split('@')
    echo isBuildNumber.size().toString()
    def jobToBuild = 1
    if (isBuildNumber.size() == 2) {
      echo isBuildNumber[1]
      jobToBuild = isBuildNumber[1].toInteger()
    }
    jobToBuild = jobToBuild
    echo 'building ' + jobToBuild
    def jobToBuildName = sprintf('EL%02dSuiteAxis', jobToBuild)
    echo jobToBuildName
  }
  stages {
    stage('setup') {
      steps {
        sh 'echo ${VAL1}'
        pwd()
        isUnix()
      }
    }
  }
  environment {
    VAL1 = 'duodieci'
  }
  triggers {
    cron('H 1 * * *')
  }
}