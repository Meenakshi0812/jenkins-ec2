pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                // clone your Git repository
                git 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
        stage('Deploy') {
            steps {
                // start the SSH agent and add your private key
                sshagent(['ssh_cred']) {
                    // copy the PHP code to the EC2 instance
                    sh "scp -r date.php ec2-user@54.167.35.145:/var/www/html/"
                }
            }
        }
    }
}
