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
                sh 'sudo scp -o StrictHostKeyChecking=no -r ./date.php ec2-user@3.95.188.119:/var/www/html'
            }
        }
    }
}
