pipeline {
    agent any
    tools {
        ansible 'ansible'
    }

    stages {
        stage ("clean workspace")
        {
            steps {
                cleanWs()
            } 
        }
        stage ("checkout")
        {
            steps {
                git branch: 'main',
                url: 'https://github.com/ash2code/Ansible-EC2.git'
            }
        }  
        stage ('TRIVY FS SCAN') 
        {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage ("ansible provision")
        {
            steps {
                sh "pip install --upgrade requests==2.20.1"
                ansiblePlaybook playbook: 'ec2provision.yaml'
                extras: "-e 'ansible_python_interpreter=/usr/bin/python3'"
            }

        }
    }
}
