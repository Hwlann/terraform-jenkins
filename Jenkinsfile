properties([pipelineTriggers([githubPush()])])

pipeline {
    agent { 
      docker {
        image 'hashicorp/terraform'
        args  '--entrypoint='
      }
    }
    
    stages {
        stage('Init') {
            steps {
                sh 'cd /home/ubuntu/terraform-jenkins && terraform init'
            }
        }
        stage('Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('Apply') {
           steps {
              sh 'terraform apply -auto-approve'
           }
        }
    }
}
