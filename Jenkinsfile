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

        stage('NPM Dependency audit') {
            steps {
                sh 'npm audit --audit-level=critical'
            }
        }
    }
    post {
        success {
            echo 'successfull'
        }
    }
}