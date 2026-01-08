pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'my-jenkins-deploy-bucket12'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Static website - no build required'
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                     credentialsId: 'aws-s3-creds',
                     accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                     secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']
                ]) {
                    sh '''
                      aws sts get-caller-identity
                      aws s3 sync . s3://$S3_BUCKET \
                        --exclude ".git/*" \
                        --exclude "Jenkinsfile" \
                        --delete
                    '''
                }
            }
        }
    }
}
