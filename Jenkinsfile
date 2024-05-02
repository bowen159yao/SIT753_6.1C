 pipeline {
    agent any // This specifies that the pipeline can run on any available agent

    stages {
        stage('Build') {
            steps {
                script {
                    // Assuming you're using Maven as the build tool
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit and integration tests, possibly with Maven
                    sh 'mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Example: Using SonarQube for code quality analysis
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Example: Using OWASP Dependency Check
                    sh 'mvn org.owasp:dependency-check-maven:check'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Deploy to a staging server, example using a script
                    sh './deploy-staging.sh'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on the staging server
                    sh 'curl -s http://staging-server-url/api/v1/tests'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy to the production server
                    sh './deploy-production.sh'
                }
            }
        }
    }

    post {
        always {
            // Send notification or perform some cleanup tasks
            echo 'Pipeline execution is complete!'
        }
    }
}

