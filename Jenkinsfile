@Library('github.com/releaseworks/jenkinslib') _
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
           withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-key', usernameVariable: 'AKIAXEQG34BCOLERK5PK', passwordVariable: '20k9zV+65inlceUveVr5My+bYuDFMhm1qCzcY9Fv']]) {
                AWS("--region=eu-west-3 s3 ls")
                steps {
                    sh 'terraform plan'
                }
            }
        }
        stage('Apply') {
           withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-key', usernameVariable: 'AKIAXEQG34BCOLERK5PK', passwordVariable: '20k9zV+65inlceUveVr5My+bYuDFMhm1qCzcY9Fv']]) {
               AWS("--region=eu-west-3 s3 ls")
               steps {
                  sh 'terraform apply -auto-approve'
               }
           }
        }
    }
}
