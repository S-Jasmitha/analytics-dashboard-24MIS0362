pipeline {
    agent any

    environment {
        DOCKERHUB_REPO = 'YOUR_DOCKERHUB_USERNAME/analytics-dashboard'
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build V1') {
            steps { sh 'docker build -t $DOCKERHUB_REPO:v1 ./v1' }
        }
        stage('Build V2') {
            steps { sh 'docker build -t $DOCKERHUB_REPO:v2 ./v2' }
        }
        stage('Build V3') {
            steps { sh 'docker build -t $DOCKERHUB_REPO:v3 ./v3' }
        }
        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DH_USER', passwordVariable: 'DH_TOKEN')]) {
                    sh '''
                      echo "$DH_TOKEN" | docker login -u "$DH_USER" --password-stdin
                      docker push "$DOCKERHUB_REPO:v1"
                      docker push "$DOCKERHUB_REPO:v2"
                      docker push "$DOCKERHUB_REPO:v3"
                      docker logout
                    '''
                }
            }
        }
    }
}
