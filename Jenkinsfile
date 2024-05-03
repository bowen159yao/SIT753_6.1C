pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'notify@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven.'
                bat 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                bat 'mvn test > test_results.log'
            }
            post {
                always {
                    emailext(
                        to: '${env.EMAIL_RECIPIENTS}',
                        subject: "${env.JOB_NAME} - Test Stage Completed",
                        body: "The test stage has completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "test_results.log"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube.'
                bat 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'mvn org.owasp:dependency-check-maven:check > security_scan.log'
            }
            
            post {
                always {
                    emailext(
                        to: '${env.EMAIL_RECIPIENTS}',
                        subject: "${env.JOB_NAME} - Security Scan Stage Completed",
                        body: "The security scan stage has completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "security_scan.log"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploy application to AWS EC2 staging environment.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on the staging environment.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploy application to AWS EC2 production environment.'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
    
}
