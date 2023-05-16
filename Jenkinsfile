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
                        ssh -i /Users/meenakshigowra/downloads/keypairs/jenkins.cer ec2-user@107.22.129.135 'cd /var/www/html && git pull'
                    """
                }
            }
        }
    }
}
