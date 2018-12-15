pipeline {
  agent any

  triggers { pollSCM('*/15 * * * *') }

  stages {

    stage('deps') {
      steps {
        sh 'git submodule init'
        sh 'git submodule update'
      }
    }

    stage('build') {
      steps {
        sh 'hugo'
      }
    }
    stage('deploy') {
      when {
        branch 'master'
      }

      steps {
        sh 'rsync -rlt --del public/ webdeploy@com1.larch.space:/usr/local/www/littlesunfarm.com/'
      }
    }
  }
}
