pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
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
    stage('stage 1') {
      steps {
        parallel(
          "erp": {
            sh 'echo ${VAL1}'
            pwd()
            isUnix()
            
          },
          "retail.core": {
            echo 'step 2'
            
          }
        )
      }
    }
    stage('Example Build') {
      steps {
        echo 'Hello World'
        build 'Freestyle'
      }
    }
    stage('Example Deploy') {
      when {
        expression {
          BRANCH_NAME ==~ /(production|staging)/
        }
        
        anyOf {
          environment name: 'DEPLOY_TO', value: 'production'
          environment name: 'DEPLOY_TO', value: 'staging'
        }
        
      }
      steps {
        echo 'Deploying'
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