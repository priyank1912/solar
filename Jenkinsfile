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
                        dependencyCheck additionalArguments: '''
                            --scan \'./\'
                            --out \'./\'
                            --format \'ALL\'
                            --prettyPrint''', odcInstallation: 'Owasp'
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
