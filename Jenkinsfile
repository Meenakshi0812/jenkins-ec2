pipeline {
    agent any
    environment {
        SERVER_IP = "54.167.35.145" // Replace with your EC2 instance IP address
        SSH_CRED_ID = "ssh_cred" // Replace with your SSH credential ID
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Meenakshi0812/jenkins-ec2.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Build steps go here"'
                // Replace this with your actual build commands
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials: [SSH_CRED_ID]) {
                    sh "scp -r ./* ec2-user@${SERVER_IP}:/var/www/html/"
                }
            }
        }
    }
}
