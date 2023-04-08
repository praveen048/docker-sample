pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-new')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/praveen048/docker-sample.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t praveen/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push praveen/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

