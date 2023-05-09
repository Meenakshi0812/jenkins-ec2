pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your code repository
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'ssh_cred', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git']]])
            }
        }
        stage('Deploy') {
            environment {
                // Define the SSH credentials for your EC2 instance
                SSH_KEY = credentials('ssh_cred')
            }
            steps {
                // Authenticate SSH agent with your EC2 instance
                sshagent(['ssh_cred']) {
                    // Copy your PHP code to the remote server
                    sh "scp -o 'StrictHostKeyChecking=no' -r /home/ec2-user/jenkins-ec2/date.php ec2-user@172.31.23.221:/var/www/html/"
                  }
            }
        }
    }
}
