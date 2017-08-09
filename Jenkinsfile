pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('setup') {
      steps {
        echo 'setup'
        sh 'mkdir -p artifacts'
        echo 'workspace: ${WORKSPACE}'
      }
    }
    stage('initialize') {
      steps {
        parallel(
          "stop tomcat": {
            echo 'stop tomcat'
            sh 'touch artifacts/tomcatStartedLog'
            archiveArtifacts(artifacts: 'artifacts/**', fingerprint: true)
            
          },
          "etc": {
            echo 'etc'
            
          }
        )
      }
    }
    stage('clone repos') {
      steps {
        parallel(
          "erp": {
            sh 'echo ${REPO_ERP}'
            sh 'mkdir -p ${CONTEXT}'
            sh 'hg update -R ${CONTEXT}'
            
          },
          "modules": {
            echo 'cloning modules'
            sh 'hg update -R ${CONTEXT}/modules/org.openbravo.util.db'
            
          },
          "Build Clone Repos": {
            # build(job: '../jenkinsPipelinesCloneRepos/master', quietPeriod: 2)
            
          }
        )
      }
    }
    stage('compile') {
      steps {
        sh 'cd ${CONTEXT} && ant clean'
      }
    }
    stage('start hwmanager') {
      steps {
        echo 'start hwmanager'
      }
    }
    stage('execute tests') {
      steps {
        parallel(
          "suite 001": {
            echo 'suite 001'
            build 'Freestyle'
            sh 'touch artifacts/suite001report'
            archiveArtifacts(artifacts: 'artifacts/**', fingerprint: true)
            
          },
          "suite 002": {
            echo 'suite 002'
            build 'Freestyle'
            sh 'touch artifacts/suite002report'
            archiveArtifacts(artifacts: 'artifacts/**', fingerprint: true)
            
          }
        )
      }
    }
    stage('create report') {
      steps {
        echo 'create report'
      }
    }
    stage('release resources') {
      steps {
        echo 'release resources'
      }
    }
  }
  environment {
    WORKSPACE = pwd()
    CONTEXT = 'context'
    REPO_ERP = 'https://code.openbravo.com/erp/devel/pi'
    REPO_MODULES = 'https://code.openbravo.com/erp/mods/org.openbravo.util.db'
  }
  triggers {
    cron('H 1 * * *')
  }
}