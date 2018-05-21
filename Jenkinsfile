pipeline {
  agent {
    docker {
      args '--tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --security-opt seccomp=unconfined'
      image 'sedunne/docker-centos7-ansible:latest'
    }

  }
  stages {
    stage('Lint') {
      steps {
        sh 'ansible-lint -v ./'
      }
    }
    stage('Deps') {
      steps {
        sh 'python tests/deps.py'
        sh '/bin/bash -c "if [ -e tests/requirements.yml ]; then ansible-galaxy install -r tests/requirements.yml -p tests/roles; fi"'
      }
    }
    stage('Run Playbook') {
      steps {
        sh 'ansible-playbook tests/jenkins.yml'
      }
    }
  }
  environment {
    ANSIBLE_ROLES_PATH = 'tests/roles'
  }
}