pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
        
        stage('Deploy Code to EC2 Instance') {
            steps {
                sh 'ssh -i  /Users/meenakshigowra/downloads/keypairs/jenkins.cer ec2-user@3.95.188.119 "sudo cp -r  /home/ec2-user/jenkins-ec2/date.php  /var/www/html"'
            }
        }
    }
}
