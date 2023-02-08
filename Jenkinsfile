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

      /*  stage('Create EC2') {
            steps {
                // execute ansible playbook
                //ansiblePlaybook playbook: 'create-ec2.yaml'
                ansiblePlaybook installation: 'Ansible',  playbook: 'create-ec2.yaml'
            }
        }*/

        stage('Configure FortiGate') {
            steps {
                // execute ansible playbook to create dynamic object
                ansiblePlaybook installation: 'Ansible', inventory: 'fgt-hosts', playbook: 'custom-api-dyn-addr.yaml'
                // execute ansible playbook to security policy
                ///ansiblePlaybook installation: 'Ansible', inventory: 'fgt-hosts', playbook: 'sec-policy.yaml'
            }
        }
    }
}