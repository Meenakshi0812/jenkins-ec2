pipeline {
    agent any
    
    environment {
        EC2_INSTANCE_IP = '54.167.35.145'
        EC2_INSTANCE_USER = 'ec2-user'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['aws-keypair.pem']) {
                    sh "scp -r ./dist/* ${EC2_INSTANCE_USER}@${EC2_INSTANCE_IP}:/var/www/html"
                }
            }
        }
    }
}
