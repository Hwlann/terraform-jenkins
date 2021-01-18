@Library('github.com/releaseworks/jenkinslib') _
node {
  stage("AWS Configure") {
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-key', usernameVariable: 'AKIAXEQG34BCOLERK5PK', passwordVariable: '20k9zV+65inlceUveVr5My+bYuDFMhm1qCzcY9Fv']]) {
        AWS("--region=eu-west-3 s3 ls")
    }
  }
}



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
                sh 'terraform init'
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
