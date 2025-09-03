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
        stage('scanning dependencies') {
            parallel{
                stage('NPM Dependency audit') {
                    steps {
                        sh 'npm audit --audit-level=critical'
                    }
                }
                stage("owasp dependency check") {
                    steps {
                        dependencyCheck additionalArguments: '--scan ./ --format "ALL" --project "my-project" --out .', odcInstallation: 'dependency-check'
                    }
                }   
            }
        }
    }
    post {
        success {
        echo 'successfull'
        }
    }
}
