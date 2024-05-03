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
                    mail to: "bowenyao159@gmail.com",
                    subject: "Build Status Email",
                    body: "Build log attached!"
                    attachmentsPattern: '**/*.log'
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
                    mail to: "bowenyao159@gmail.com",
                    subject: "Build Status Email",
                    body: "Build log attached!"
                    attachmentsPattern: '**/*.log'
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
