pipeline {
    agent any

    environment {
        SERVER_IP = "10.27.1.177"
        DEPLOY_DIR = "/usr/share/nginx/html/team-php-notes"
    }

    stages {
        stage('Deploy to Oracle') {
            steps {
                sshagent(['oracle-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no opc@$SERVER_IP << EOF
                      sudo -i
                      cd $DEPLOY_DIR
                      git pull origin develop
                      sudo systemctl restart nginx || true
                    EOF
                    '''
                }
            }
        }
    }
}
