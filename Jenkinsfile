pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build the application using Maven.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    try {
                        sh 'mvn test > test_results.log'
                        echo 'Tests succeeded.'
                    } catch (Exception e) {
                        echo 'Tests failed.'
                        throw e // Re-throw exception to mark stage as failed
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "${env.JOB_NAME} - Test Stage Completed",
                        body: """<p>Test stage completed. Check the attached log for details.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        attachmentsPattern: "**/test_results.log",
                        to: "${env.EMAIL_RECIPIENTS}"
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyze code with SonarQube.'
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        sh 'mvn org.owasp:dependency-check-maven:check > security_scan.log'
                        echo 'Security scan succeeded.'
                    } catch (Exception e) {
                        echo 'Security scan failed.'
                        throw e // Re-throw exception to mark stage as failed
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "${env.JOB_NAME} - Security Scan Stage Completed",
                        body: """<p>Security scan stage completed. Check the attached log for details.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        attachmentsPattern: "**/security_scan.log",
                        to: "${env.EMAIL_RECIPIENTS}"
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
                echo 'Run integration tests on the staging environment using Selenium.'
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

