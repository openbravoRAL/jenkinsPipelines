pipeline {
  agent {
    node {
      label 'master'
    }
    
  }

  stages {
    stage('setup') {
      steps {

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
    }
    stage('stage 1') {
      steps {
        sh 'echo ${VAL1}'
        pwd()
        isUnix()
      }
    }
  }
  environment {
    VAL1 = 'duodieci'
    workspace = pwd()
  }
  triggers {
    cron('H 1 * * *')
  }
}