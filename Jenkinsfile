pipeline {
    agent {
        node {
            label 'slaveJENKINS'
        }
    }
environment {
    TERRAFORM_CMD = 'sudo docker run --network host -w /app -v /root/.aws:/root/.aws -v /root/.ssh:/root/.ssh -v "${WORKSPACE}":/app hashicorp/terraform:light'

    }
      	stages {
          stage('checkout repo') {
            steps {
              git url: 'https://github.com/toketunji/tack.git'
            }
          }
	
          stage('pull latest light terraform image') {
	    steps {
              withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
                sh  """
                    sudo docker pull hashicorp/terraform:light
                    """
              }
            }
          }
          stage('Install Kubernestes Cluster') {
            steps {
              ansiColor('xterm') {
               withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
                sh  """
                    make all
                    """
              }
              }
            }
          }
}
