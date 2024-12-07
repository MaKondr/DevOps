pipeline {
    agent any
    environment {
        GIT_REPO = 'git@github.com:MaKondr/DevOps.git' // URL вашего репозитория
        ANSIBLE_PLAYBOOK = 'playbook.yml' // Ваш Ansible playbook
        GIT_CREDENTIALS_ID = '25073fda-2ef6-4dda-8c81-ef63bcba064f' // ID SSH ключа для Git
        ANSIBLE_CREDENTIALS_ID = 'ansible_ssh_key' // ID SSH ключа для Ansible
    }
    stages {
        stage('Install Ansible') {
            steps {
                script {
                    // Устанавливаем Ansible в контейнере
                    sh 'apt-get update && sudo apt-get install -y ansible'
                }
            }
        }
        stage('Clone Repository') {
            steps {
                git credentialsId: "${GIT_CREDENTIALS_ID}", branch: 'master', url: "${GIT_REPO}" // Клонирование репозитория
            }
        }
        stage('Run Ansible') {
            steps {
                script {
                    sh 'cd ansible-step-by-step'
                }
                ansiblePlaybook(
                    playbook: "${ANSIBLE_PLAYBOOK}",   // Файл playbook в репозитории
                    inventory: 'inventory.yml', // Инвентори-файл
                    credentialsId: 'ansible_ssh_key'  // ID SSH ключа из Credentials
                )
            }
        }
    }
}
