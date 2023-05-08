pipeline {
    agent any
    environment {
        SSH_KEY = credentials('aws-keypair.pem')
        EC2_INSTANCE_USER = 'ec2-user'
        EC2_INSTANCE_IP = '54.167.35.145'
        REPO_NAME = 'jenkins-ec2'
        PHP_CODE_PATH = 'path/to/your-php-code'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: "https://github.com/<your-github-username>/${REPO_NAME}.git"]]])
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['$SSH_KEY']) {
                    sh "scp -r ./${PHP_CODE_PATH}/* ${EC2_INSTANCE_USER}@${EC2_INSTANCE_IP}:/var/www/html"
                }
            }
        }
    }
}
