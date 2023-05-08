pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git'
            }
        }
        stage('Upload to S3') {
            steps {
                sh 'aws s3 cp . s3://jenkins-ec2/my-app --recursive'
            }
        }
        stage('Copy to EC2') {
            steps {
                withAWS(region:'us-east-1', credentials:'aws-creds') {
                    sh 'aws s3 cp s3://jenkins-ec2/my-app . --recursive'
                    sshagent(['aws-keypair']) {
                        sh 'ssh -i "aws-keypair.pem" ec2-user@ec2-54-167-35-145.compute-1.amazonaws.com "sudo cp -r . /var/www/html"'
                    }
                }
            }
        }
    }
}

