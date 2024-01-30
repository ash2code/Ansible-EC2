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
                ansiblePlaybook playbook: 'ec2provision.yaml'
            }

        }
    }
}
