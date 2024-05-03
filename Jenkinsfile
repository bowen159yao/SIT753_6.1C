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
                echo 'Testing ...'
            }
            post {
                always {
                    emailext(
                        to: 'bowenyao159@gmail.com',
                        subject: "${env.JOB_NAME} - Test Results",
                        body: "Unit and Integration Test stage completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "**/target/surefire-reports/*.txt,**/target/failsafe-reports/*.txt"
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
                echo 'Scanning ...'
            }
            
            post {
                always {
                    emailext(
                        to: 'bowenyao159@gmail.com',
                        subject: "${env.JOB_NAME} - Test Results",
                        body: "Unit and Integration Test stage completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "**/target/surefire-reports/*.txt,**/target/failsafe-reports/*.txt"
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
