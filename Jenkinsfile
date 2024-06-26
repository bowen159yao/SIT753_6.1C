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
                success {
                    emailext (
                        attachLog: true,
                        to: 'bowenyao159@gmail.com',
                        subject: "SUCCESS: Test Stage - ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "The Test stage completed successfully.",
                        attachmentsPattern: '**/log'
                    )
                }
                failure {
                    emailext (
                        attachLog: true,  
                        to: 'bowenyao159@gmail.com',
                        subject: "FAILURE: Test Stage - ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "The Test stage failed. See attached logs for more details.",
                        attachmentsPattern: '**/log'
                    )
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
                success {
                    emailext (
                        attachLog: true,
                        to: 'bowenyao159@gmail.com',
                        subject: "SUCCESS: Security Scan Stage - ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "The Security Scan stage completed successfully.",
                        attachmentsPattern: '**/log'
                    )
                }
                failure {
                    emailext (
                        attachLog: true,
                        to: 'bowenyao159@gmail.com',
                        subject: "FAILURE: Security Scan Stage - ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "The Security Scan stage failed. See attached logs for more details.",
                        attachmentsPattern: '**/log'
                    )
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
