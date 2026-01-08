pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Static website - no build required'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://jenkins-automation-s3-bucket \
                --exclude ".git/*" \
                --exclude "Jenkinsfile" \
                --delete
                '''
            }
        }
    }
}
