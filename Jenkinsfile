#!groovy

node ('ansible_slave') {
    git poll: true, url: '${TEMPLATES_GIT_URL}'

    timestamps {
        
    stage('Clean dir before start') {
        dir("ansible") {
            sh 'rm -rf ./*'
        }
    }
    stage('Get data from GIT') {
        dir("ansible") {
            git poll: false, url: "${PLAYBOOK_GIT_URL}"
        }
            git url: "${TEMPLATES_GIT_URL}"
            sh 'mv ./templates ./vars ./ansible/roles/nginx'
    }

    stage('Validation of playbook') {
        dir("ansible") {
            sh 'ansible-playbook --syntax-check --list-tasks "${PLAYBOOK_PATH}"'
        }
    }
    stage('Run playbook') {
        dir("ansible") {
            sh 'ansible-playbook "${PLAYBOOK_PATH}"'
        }
    }
    }
}
