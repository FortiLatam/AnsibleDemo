pipeline {
    agent any

    stages {
        
        stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        } 

        stage('execute') {
            steps {
                // execute ansible playbook
                //ansiblePlaybook playbook: 'create-ec2.yaml'
                ansiblePlaybook installation: 'Ansible',  playbook: 'create-ec2.yaml'
            }
        }
    }
}