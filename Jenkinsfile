pipeline {
    agent any
    environment {
        GIT_REPO = 'git@github.com:MaKondr/DevOps.git' // URL вашего репозитория
        PATH_TO_ADS = 'ansible-step-by-step' // Папка с Ansible playbook
        GIT_CREDENTIALS_ID = '25073fda-2ef6-4dda-8c81-ef63bcba064f' // ID SSH ключа для Git
        ANSIBLE_CREDENTIALS_ID = 'c3a3dcae-ed4a-4a9b-a980-e65afcb2d4c7' // ID SSH ключа для Ansible
    }
    stages {
        stage('Preparing the environment') {
            steps {
                // Клонирование репозитория
                git credentialsId: "${GIT_CREDENTIALS_ID}", branch: 'master', url: "${GIT_REPO}"
                // Запуск ansible playbook с тегами
                ansiblePlaybook(
                    playbook: "${PATH_TO_ADS}/playbook.yml",  // Путь к playbook
                    inventory: "${PATH_TO_ADS}/inventory.yml", // Путь к инвентори-файлу
                    credentialsId: "${ANSIBLE_CREDENTIALS_ID}", // ID SSH ключа для Ansible
                    tags: 'clone, docker'  // Теги, которые должны быть выполнены
                )
            }
        }
        stage('Launch service') {
            steps {
                // Запуск другого playbook с тегом 'start'
                ansiblePlaybook(
                    playbook: "${PATH_TO_ADS}/playbook.yml",  // Путь к playbook
                    inventory: "${PATH_TO_ADS}/inventory.yml", // Путь к инвентори-файлу
                    credentialsId: "${ANSIBLE_CREDENTIALS_ID}", // ID SSH ключа для Ansible
                    tags: 'start'  // Тег для запуска
                )
            }
        }
    }
}
