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
                    sh "scp -r ./your-php-code.php ec2-user@your-ec2-instance-public-ip:/var/www/html/"
                }
            }
        }
    }
}
