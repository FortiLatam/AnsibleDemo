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

        stage('SAST'){
            steps {
                 sh 'env | grep -E "JENKINS_HOME|BUILD_ID|GIT_BRANCH|GIT_COMMIT" > /tmp/env'
                 sh 'docker pull registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
                 sh 'docker run --rm --env-file /tmp/env --mount type=bind,source=$PWD,target=/scan registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
            }
        }
        
        stage('Create EC2') {
            steps {
                // execute ansible playbook
                //ansiblePlaybook playbook: 'create-ec2.yaml'
                ansiblePlaybook installation: 'Ansible',  playbook: 'create-ec2.yaml'
            }
        }

        stage('Configure FortiGate') {
            steps {
                // execute ansible playbook to create dynamic object
                ansiblePlaybook installation: 'Ansible', inventory: 'fgt-hosts', playbook: 'custom-api-dyn-addr.yaml'
                // execute ansible playbook to security policy
                ansiblePlaybook installation: 'Ansible', inventory: 'fgt-hosts', playbook: 'sec-policy.yaml'
            }
        }
    }
}