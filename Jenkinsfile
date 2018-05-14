pipeline {
  agent {
    docker {
      image 'sedunne/docker-centos7-ansible'
      args 'http://localhost:8080/blue/organizations/jenkins/pipeline-editor/ansible-role-nginx/jenkins/'
    }

  }
  stages {
    stage('Test') {
      steps {
        sh 'pwd && ls'
      }
    }
  }
}