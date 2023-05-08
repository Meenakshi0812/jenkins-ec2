pipeline {
  agent any
  
  environment {
    AWS_DEFAULT_REGION = 'us-east-1'
    AWS_S3_BUCKET = 'jenkins-ec2'
    EC2_INSTANCE_IP_ADDRESS = '54.167.35.145'
    SSH_USERNAME = 'ec2-user'
    SSH_KEY_FILE = '/var/lib/jenkins/ssh/aws-keypair.pem'
  }
  
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ec2.git'
      }
    }
    stage('Maven build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Deploy to EC2') {
      steps {
        sh "aws s3 sync ./target s3://${AWS_S3_BUCKET}/ --delete"
        sshagent(['aws-keypair']) {
          sh "ssh -o StrictHostKeyChecking=no -i ${SSH_KEY_FILE} ${SSH_USERNAME}@${EC2_INSTANCE_IP_ADDRESS} sudo rm -rf /var/www/html/*"
          sh "ssh -o StrictHostKeyChecking=no -i ${SSH_KEY_FILE} ${SSH_USERNAME}@${EC2_INSTANCE_IP_ADDRESS} sudo aws s3 sync s3://${AWS_S3_BUCKET}/ /var/www/html"
        }
      }
    }
  }
}

