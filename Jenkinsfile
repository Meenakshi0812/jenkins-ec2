pipeline {
    agent any

    environment {
        EC2_INSTANCE_IP = '54.167.35.145'
        EC2_INSTANCE_USER = 'ec2-user'
        REPO_NAME = 'jenkins-ec2'
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: BRANCH_NAME, url: "https://github.com/Meenakshi0812/${REPO_NAME}.git"
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sshagent(['ssh_cred']) {
                        sh "scp -r ./${REPO_NAME}/. ${EC2_INSTANCE_USER}@${EC2_INSTANCE_IP}:/var/www/html"
                    }
                }
            }
        }
    }
}
