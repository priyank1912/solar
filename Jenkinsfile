pipeline {
    agent any
    options {
        timestamps()
    }
    stages {
        stage('Check node version') {
            steps {
                sh '''
                node -v
                npm -v
                '''
            }
        }
    }
    post {
        success {
            echo 'successfull'
        }
    }
}