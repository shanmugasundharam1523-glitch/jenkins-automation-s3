pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Static website - no build required'
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-s3-creds',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    sh '''
                    aws sts get-caller-identity
                    aws s3 sync . s3://jenkins-automation-s3-bucket \
                      --exclude ".git/*" \
                      --exclude "Jenkinsfile" \
                      --delete
                    '''
                }
            }
        }
    }
}
