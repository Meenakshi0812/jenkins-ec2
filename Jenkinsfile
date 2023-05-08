pipeline {
    agent any
    environment {
        SSH_KEY = credentials('ssh_cred')
        SSH_HOST = 'ec2-54-167-35-145.compute-1.amazonaws.com'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], 
                          userRemoteConfigs: [[url: 'https://github.com/Meenakshi0812/jenkins-ec2.git']]])
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-ec2-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    withEnv(['SSH_AUTH_SOCK' + '= $SSH_AUTH_SOCK', 'SSH_AGENT_PID' + '= $SSH_AGENT_PID']) {
                        sh 'ssh-keyscan $SSH_HOST >> ~/.ssh/known_hosts'
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "scp -r './home/ec2-user/jenkins-ec2/*' ec2-user@$SSH_HOST:/var/www/html/"
                        }
                    }
                }
            }
        }
    }
}
