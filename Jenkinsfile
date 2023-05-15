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
        sh '''
          ssh -i /Users/meenakshigowra/downloads/keypairs/jenkins.cer ec2-user@107.22.129.135 "sudo rm -rf /var/www/html/*"
          scp -i /Users/meenakshigowra/downloads/keypairs/jenkins.cer -r /home/ec2-user/jenkins-ec2/date.php/* ec2-user@107.22.129.135:/var/www/html/
        '''
      }
    }
  }
}
