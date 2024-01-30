pipeline {
  agent any
  tools {
    ansible 'ansible'
  }

  stages {
    stage('Clean workspace') {
      steps {
        cleanWs()
      }
    }

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/ash2code/Ansible-EC2.git'
      }
    }

    stage('TRIVY FS SCAN') {
      steps {
        sh "trivy fs . > trivyfs.txt"
      }
    }

    stage('Ansible provision') {
      steps {
        ansiblePlaybook(
          playbook: 'ec2provision.yaml',
          extras: '-e ansible_python_interpreter=/path/to/correct/python'  // Specify if needed
        )
      }
    }
  }
}
