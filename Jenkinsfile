pipeline {
  agent {
    docker {
      image 'sedunne/docker-centos7-ansible'
      args '--tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --security-opt seccomp=unconfined'
    }

  }
  stages {
    stage('Init') {
      steps {
        echo 'First Test'
      }
    }
  }
}