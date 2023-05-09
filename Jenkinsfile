pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
        
        stage('Deploy Code to EC2 Instance') {
            steps {
                sh 'sudo scp -o StrictHostKeyChecking=no -r ./date.php ec2-user@ip-172-31-90-152:/var/www/html'
            }
        }
    }
}
