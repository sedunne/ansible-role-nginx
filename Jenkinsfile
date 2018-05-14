pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'cd $WORKSPACE && /bin/bash tests/test.sh'
      }
    }
  }
}