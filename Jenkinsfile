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

                        dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true

                        publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, icon: '', keepAll: true, reportDir: './', reportFiles: 'dependency-check-jenkins.html', reportName: 'dependency-check-jenkins.html', reportTitles: '', useWrapperFileDirectly: true])
                    }
                }   
            }
        }
        stage('Unit testing') {
            steps {
                sh 'npm test'
            }
        }
    }
    post {
        success {
        echo 'successfull'
        }
    }
}
