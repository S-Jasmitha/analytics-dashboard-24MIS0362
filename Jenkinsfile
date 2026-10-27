
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'GitHub source code checked out by Jenkins'
            }
        }

        stage('Verify V1') {
            steps {
                bat 'dir v1'
                bat 'if exist v1\\index.html (echo V1 files verified) else (exit 1)'
            }
        }

        stage('Verify V2') {
            steps {
                bat 'dir v2'
                bat 'if exist v2\\index.html (echo V2 files verified) else (exit 1)'
            }
        }

        stage('Verify V3') {
            steps {
                bat 'dir v3'
                bat 'if exist v3\\index.html (echo V3 files verified) else (exit 1)'
            }
        }

        stage('Verify Docker') {
            steps {
                bat 'docker --version'
            }
        }
    }

    post {
        success {
            echo 'Analytics Dashboard pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
