pipeline {
    agent any
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
                sshagent(['ssh-public-key-local']) {
                    sh "cd /Users/meenakshigowra/downloads/keypairs ssh -i "jenkins.cer" ec2-user@ec2-107-22-129-135.compute-1.amazonaws.com 'sudo systemctl stop myapp.service && sudo rm -rf /var/www/html/* && sudo cp -r /var/lib/jenkins/workspace/myapp/dist/* /var/www/html/ && sudo systemctl start myapp.service'"
                }
            }
        }
    }
}
