pipeline {
  agent {
    docker {
      args 'http://localhost:8080/blue/organizations/jenkins/pipeline-editor/ansible-role-nginx/jenkins/'
      image 'sedunne:docker-centos7-ansible'
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