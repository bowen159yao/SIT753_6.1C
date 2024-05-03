pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'

            }
            post {
                always {
                    emailext (
                        to: 'bowenyao159@gmail.com',
                        subject: 'Security Scan Stage Failure',
                        body: 'Security scan stage failed.',
                        attachmentsPattern: 'logs/*.log'
                        ）
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
            }
            post {
                always {
                    emailext (
                        to: 'bowenyao159@gmail.com',
                        subject: 'Security Scan Stage Failure',
                        body: 'Security scan stage failed.',
                        attachmentsPattern: 'logs/*.log'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to AWS EC2 staging environment.'

            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment.'

            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to AWS EC2 production environment.'

            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}
