properties([pipelineTriggers([githubPush()])])

pipeline {
    agent { 
      docker {
        image 'hashicorp/terraform'
        args  '--entrypoint='
      }
    }
    
    stages {
        stage("AWS Configure") {
            withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-key', usernameVariable: 'AKIAXEQG34BCFFJS43NW', passwordVariable: 'mECJbXX4v+UwzntzNVEXW32XC7LSp6yiTD5kNUgI']]) {
                AWS("--region=eu-west-3 s3 ls")
            }
        }
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
