stage('Deploy to S3') {
    steps {
        withCredentials([
            [
                $class: 'AmazonWebServicesCredentialsBinding',
                credentialsId: 'aws-s3-creds',
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
            ]
        ]) {
            sh '''
              aws configure set region us-east-1
              aws sts get-caller-identity
              aws s3 ls
              aws s3 sync . s3://my-jenkins-deploy-bucket12 \
                --exclude ".git/*" \
                --exclude "Jenkinsfile" \
                --delete
            '''
        }
    }
}
