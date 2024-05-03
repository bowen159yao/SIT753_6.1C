pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'notify@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build the application using Maven.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Run unit and integration tests using JUnit and Selenium.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyze code with SonarQube.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Perform security scan with OWASP Dependency Check.'
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
            emailext (
                to: "${env.EMAIL_RECIPIENTS}",
                subject: "Jenkins Pipeline Status: ${env.JOB_NAME} - ${currentBuild.currentResult}",
                body: """<p>Pipeline execution of ${env.JOB_NAME} has completed.</p>
                         <p>Status: ${currentBuild.currentResult}</p>""",
                attachmentsPattern: "**/test_results.log,**/security_scan.log"
            )
        }
    }
    
}
