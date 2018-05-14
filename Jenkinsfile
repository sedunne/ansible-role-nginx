pipeline {
  agent {
    docker {
      image 'sedunne/docker-centos7-ansible:latest'
      args '--tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --security-opt seccomp=unconfined'
    }

  }
  stages {
    stage('Prep') {
      steps {
        sh 'python tests/deps.py'
        sh '/bin/bash -c "if [ -e tests/requirements.yml ]; then ansible-galaxy install -r tests/requirements.yml; fi"'
      }
    }
    stage('Verify') {
      steps {
        sh 'ls tests'
      }
    }
  }
}