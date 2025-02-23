pipeline {
    agent any

    environment {
        ANSIBLE_PLAYBOOK = 'install_docker.yml'  // Playbook filename
        INVENTORY_FILE = 'inventory.ini'         // Inventory file
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    echo 'Pulling latest code from repository...'
                    checkout scm
                }
            }
        }

        stage('Install Ansible') {
            steps {
                script {
                    echo 'Installing Ansible on Jenkins Node...'
                    sh '''
                    sudo apt update
                    sudo apt install -y ansible
                    ansible --version
                    '''
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    echo 'Executing Ansible Playbook to configure Docker...'
                    sh '''
                    ansible-playbook -i ${INVENTORY_FILE} ${ANSIBLE_PLAYBOOK}
                    '''
                }
            }
        }
    }
}
