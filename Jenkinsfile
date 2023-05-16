pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
       
        stage('Deploy') {
            steps {
                sshagent(['ssh-public-key']) {
                    sh """
                        cd /Users/meenakshigowra/downloads/keypairs/jenkins.cer ssh -o StrictHostKeyChecking=no ec2-user@${env.107.22.129.135} 'cd /var/www/html && git pull'
                    """
                }
            }
        }
    }
}
