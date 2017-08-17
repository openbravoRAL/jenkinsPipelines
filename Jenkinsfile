pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('shared library') {
      steps {
        script {
 import com.openbravo.HelloWorld

def awesomeVar = 'so_true'
print "look at this: ${awesomeVar}"

echo "currentBuild.number: ${currentBuild.number}"

println new HelloWorld().say()
        }
      }
    }
    stage('setup') {
      steps {
        parallel(
          "setup": {
            echo 'setup'
            sh 'mkdir -p artifacts'
            echo 'workspace: ${WORKSPACE}'
            
          }
        )
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
            
          }
        )
      }
    }
    stage('compile') {
      steps {
        parallel(
          "compile": {
            sh 'cd ${CONTEXT} && ant clean'
            
          },
          "New task": {
            echo 'new task'
            
          }
        )
      }
    }
    stage('execute other pipeline') {
      steps {
        build(job: 'Freestyle', quietPeriod: 2)
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
  post {
    always {
      sh 'touch resources/*.xml'
      junit 'resources/*.xml'
      archiveArtifacts(artifacts: 'resources/*.xml', fingerprint: true)
      
    }
    
  }
  triggers {
    cron('H 1 * * *')
  }
}