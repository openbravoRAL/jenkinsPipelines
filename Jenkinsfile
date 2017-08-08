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

      }
    }
    stage('initialize') {
      steps {
        parallel(
          "stop tomcat": {
            echo 'stop tomcat'
            sh 'touch ${ARTIFACTS}/tomcatStartedLog'
            archiveArtifacts(artifacts: '**', fingerprint: true)
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
            // TODO: if new
            // sh 'hg clone ${REPO_ERP} context'
            sh 'hg update -R ${CONTEXT}'
            
          },
          "modules": {
            echo 'cloning modules'
            // sh 'hg clone ${REPO_MODULES} '
            sh 'hg update -R ${CONTEXT}/modules/org.openbravo.util.db'
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
            sh 'touch ${ARTIFACTS}/suite001report'
            archiveArtifacts(artifacts: '**', fingerprint: true)
          },
          "suite 002": {
            echo 'suite 002'
            build 'Freestyle'
            sh 'touch ${ARTIFACTS}/suite002report'
            archiveArtifacts(artifacts: '**', fingerprint: true)
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
    ARTIFACTS = pwd()/artifacts
    CONTEXT = 'context'
    REPO_ERP = 'https://code.openbravo.com/erp/devel/pi'
    REPO_MODULES = 'https://code.openbravo.com/erp/mods/org.openbravo.util.db'
  }
  triggers {
    cron('H 1 * * *')
  }
}