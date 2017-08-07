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
            sh 'echo ${VAL1}'
            pwd()
            isUnix()
            
          },
          "modules": {
            echo 'cloning modules'
            
          }
        )
      }
    }
    stage('compile') {
      steps {
        parallel(
          "suite 001": {
            echo 'suite 001'
            
          },
          "suite 002": {
            echo 'suite 002'
            
          }
        )
      }
    }
    stage('execute tests') {
      steps {
        parallel(
          "suite 001": {
            echo 'suite 001'
            build 'Freestyle'
            
          },
          "suite 002": {
            echo 'suite 002'
            build 'Freestyle'
            
          }
        )
      }
    }
    stage('report') {
      when {
        expression {
          BRANCH_NAME ==~ /(release|main)/
        }
        
        anyOf {
          environment name: 'DEPLOY_TO', value: 'production'
          environment name: 'DEPLOY_TO', value: 'staging'
        }
        
      }
      steps {
        echo 'reporting'
        archiveArtifacts(artifacts: '**', fingerprint: true)
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