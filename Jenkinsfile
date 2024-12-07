pipeline {
    agent any
    environment {
        GIT_REPO = 'git@github.com:MaKondr/DevOps.git' // URL вашего репозитория
        ANSIBLE_PLAYBOOK = 'playbook.yml' // Ваш Ansible playbook
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${GIT_REPO}" // Клонирование репозитория
            }
        }
        stage('Run Ansible') {
            steps {
                script {
                    sh 'cd ansible-step-by-step'
                }
                ansiblePlaybook(
                    playbook: "${ANSIBLE_PLAYBOOK}",   // Файл playbook в репозитории
                    inventory: 'inventory/hosts.ini', // Инвентори-файл
                    credentialsId: 'ansible_ssh_key'  // ID SSH ключа из Credentials
                )
            }
        }
    }
}
