pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        dir(path: '$WORKSPACE') {
          sh '/bin/bash test/test.sh'
        }

      }
    }
  }
}