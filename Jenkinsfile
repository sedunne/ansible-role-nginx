pipeline {
  agent {
    docker {
      image 'sedunne/docker-centos7-ansible:latest'
      args '--tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --security-opt seccomp=unconfined'
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