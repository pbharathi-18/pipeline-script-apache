pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                sh 'zip -r apache-html-$BUILD_NUMBER.zip *'
                sh 'aws s3 cp apache-html-$BUILD_NUMBER.zip s3://cicd-jenkins-appache/'
            }
        }
        stage('CD') {
            steps {
                sh 'rm -fr *'
                sh 'aws s3 cp s3://cicd-jenkins-appache/apache-html-$BUILD_NUMBER.zip .'
                sh 'unzip apache-html-$BUILD_NUMBER.zip'
                sh 'scp index.html root@10.1.1.155:/var/www/html/'
            }
        }
    }
}
