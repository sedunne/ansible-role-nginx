pipeline {
  agent {
    docker {
      image 'centos:7'
      args '--tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro --security-opt seccomp=unconfined'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'yum makecache fast && yum -y install deltarpm epel-release initscripts && yum -y install ansible sudo which git python-pip && yum clean all'
        sh 'pip install ansible-lint'
        sh 'sed -i -e \'s/^\\(Defaults\\s*requiretty\\)/#--- \\1/\' /etc/sudoers'
        sh 'echo -e \'[local]\\nlocalhost ansible_connection=local\' > /etc/ansible/hosts'
      }
    }
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