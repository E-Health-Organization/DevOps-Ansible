pipeline {
    agent any

    environment {
        GIT_REPO = 'git@github.com:E-Health-Organization/DevOps-Ansible.git' 
        BRANCH = 'main' 
        ANSIBLE_PLAYBOOK = 'install-tomcat.yaml'  // Playbook file name
        INVENTORY_FILE = 'inventory.ini'  // Ansible inventory file
        SSH_KEY = credentials('ansible-ssh-key')
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Clone the Git repository
                    // git branch: "${BRANCH}", credentialsId: 'github-ssh-key', url: "${GIT_REPO}"

                git branch: "${BRANCH}", credentialsId: 'github-ssh-key', url: "${GIT_REPO}"
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Run Ansible playbook
                    sh """
                    ansible-playbook -i ${INVENTORY_FILE} --private-key=\$SSH_KEY ${ANSIBLE_PLAYBOOK}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Ansible Playbook executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
