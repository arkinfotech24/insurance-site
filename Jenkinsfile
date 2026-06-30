pipeline {
    agent any

    environment {
        DEPLOY_USER = 'sysadmin'
        DEPLOY_HOST = '192.168.1.181'
        DEPLOY_PATH = '/var/www/html'
        SSH_KEY = '/var/jenkins_home/.ssh/insurance_deploy_key'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Files') {
            steps {
                sh '''
                pwd
                ls -la
                test -f index.html
                '''
            }
        }

        stage('Verify SSH Key') {
            steps {
                sh '''
                ls -l ${SSH_KEY}
                chmod 600 ${SSH_KEY}
                '''
            }
        }

        stage('Deploy to Web Server') {
            steps {
                sh '''
                echo "Deploying Insurance Website..."

                scp \
                  -F /dev/null \
                  -i ${SSH_KEY} \
                  -o IdentityAgent=none \
                  -o IdentitiesOnly=yes \
                  -o PreferredAuthentications=publickey \
                  -o PubkeyAuthentication=yes \
                  -o PasswordAuthentication=no \
                  -o StrictHostKeyChecking=no \
                  index.html \
                  ${DEPLOY_USER}@${DEPLOY_HOST}:/tmp/index.html

                ssh \
                  -F /dev/null \
                  -i ${SSH_KEY} \
                  -o IdentityAgent=none \
                  -o IdentitiesOnly=yes \
                  -o PreferredAuthentications=publickey \
                  -o PubkeyAuthentication=yes \
                  -o PasswordAuthentication=no \
                  -o StrictHostKeyChecking=no \
                  ${DEPLOY_USER}@${DEPLOY_HOST} \
                  "sudo cp /tmp/index.html ${DEPLOY_PATH}/index.html && sudo systemctl restart httpd"
                '''
            }
        }
    }

    post {
        success {
            echo 'Insurance website deployed successfully.'
        }

        failure {
            echo 'Deployment failed.'
        }

        always {
            cleanWs()
        }
    }
}
