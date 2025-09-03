pipeline {
    agent any
    options {
        timestamps()
    }
    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }
    }
    post {
        success {
            echo 'successfull'
        }
    }
}