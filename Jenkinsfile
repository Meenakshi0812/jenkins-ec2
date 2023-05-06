pipeline {
    agent any
    
    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCESS_KEY_ID = credentials('AKIAXLLN4ONRKNO76ZFF')
        AWS_SECRET_ACCESS_KEY = credentials('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')
        EC2_INSTANCE_IP = '18.209.15.26'
    }

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
                sh "aws ec2 scp --recursive --exclude '.git' --exclude 'node_modules' . ec2-user@${env.EC2_INSTANCE_IP}:/var/www/html"
            }
        }
    }
}
