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
                echo "======================================"
                echo "Validating project files..."
                echo "======================================"

                pwd
                ls -la

                test -f index.html

                echo "Validation successful."
                '''
            }
        }

        stage('Verify SSH Key') {
            steps {
                sh '''
                echo "======================================"
                echo "Checking SSH key..."
                echo "======================================"

                ls -l ${SSH_KEY}

                chmod 600 ${SSH_KEY}
                '''
            }
        }

        stage('Deploy to Web Server') {
            steps {
                sh '''
                echo "======================================"
                echo "Deploying Insurance Website..."
                echo "======================================"

                scp \
                    -i ${SSH_KEY} \
                    -o IdentitiesOnly=yes \
                    -o StrictHostKeyChecking=no \
                    index.html \
                    ${DEPLOY_USER}@${DEPLOY_HOST}:/tmp/index.html

                ssh \
                    -i ${SSH_KEY} \
                    -o IdentitiesOnly=yes \
                    -o StrictHostKeyChecking=no \
                    ${DEPLOY_USER}@${DEPLOY_HOST} \
                    "sudo cp /tmp/index.html ${DEPLOY_PATH}/index.html && sudo systemctl restart httpd"

                echo "Deployment completed successfully."
                '''
            }
        }
    }

    post {
        success {
            echo "======================================"
            echo "Insurance website deployed successfully."
            echo "======================================"
        }

        failure {
            echo "======================================"
            echo "Deployment failed."
            echo "======================================"
        }

        always {
            cleanWs()
        }
    }
}
