pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'notify@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven.'
                bat 'gradle build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                bat 'gradle test'
                bat 'type build\\reports\\tests\\test-results.html > test_results.log'  // Redirecting test results to a log file
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
                bat 'gradle sonarqube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency Check with Gradle.'
                bat 'gradle dependencyCheckAnalyze'
                bat 'type build\\reports\\dependency-check-report.html > security_scan.log'  // Redirecting security scan results to a log file
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
