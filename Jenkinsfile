pipeline {
    agent any

    environment {
        DEPLOY_USER = 'sysadmin'
        DEPLOY_HOST = '192.168.1.181'
        DEPLOY_PATH = '/var/www/html'
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
                echo "Checking site files..."
                test -f index.html
                '''
            }
        }

        stage('Deploy to Web Server') {
            steps {
                sh '''
                echo "Deploying insurance site..."
                scp -o StrictHostKeyChecking=no index.html ${DEPLOY_USER}@${DEPLOY_HOST}:/tmp/index.html
                ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${DEPLOY_HOST} "sudo cp /tmp/index.html ${DEPLOY_PATH}/index.html && sudo systemctl restart httpd"
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
    }
}
