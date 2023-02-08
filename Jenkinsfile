pipeline {
    agent any

    stages {
        
        stage ("checkout") {
            steps {
                        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [],                                                     userRemoteConfigs: [[url: 'https://github.com/akannan1087/myAnsibleInfraRepo']]])         
            }
        }
        stage('execute') {
            steps {
                // execute ansible playbook
                ansiblePlaybook playbook: 'create-EC2.yml'
            }
        }
    }
}