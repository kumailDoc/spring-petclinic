pipeline {
    agent any

    triggers {
        cron('H/10 * * * 4')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/kumailDoc/spring-petclinic'
            }
        }

        stage('Build') {
            steps {
                // Add steps to build the project
                sh 'mvn clean install'
            }
        }

        stage('Generate Code Coverage Report') {
            steps {
                // Add steps to generate code coverage report using Jacoco
                sh 'mvn clean test jacoco:report'
            }
            post {
                always {
                    publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'target/site/jacoco',
                        reportFiles: 'index.html',
                        reportName: 'Code Coverage Report'
                    ])
                }
            }
        }
    }
}
