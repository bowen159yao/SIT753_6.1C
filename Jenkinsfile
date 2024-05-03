pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven.'
                bat 'mvn clean package'  // 使用 bat 替换为 sh 如果在 Unix/Linux 系统
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                bat 'mvn test'  // 这里假设是在 Windows 上运行
            }
            post {
                always {
                    emailext(
                        to: 'bowenyao159@gmail.com',
                        subject: "${env.JOB_NAME} - Unit and Integration Test Results",
                        body: "The testing stage has completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "**/target/surefire-reports/*.html,**/target/failsafe-reports/*.html"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube.'
                bat 'mvn sonar:sonar'  // 添加实际的 SonarQube 分析命令
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                bat 'mvn verify -Psecurity'  // 假设有一个 Maven Profile 名为 security
            }
            post {
                always {
                    emailext(
                        to: 'bowenyao159@gmail.com',
                        subject: "${env.JOB_NAME} - Security Scan Results",
                        body: "The security scan stage has completed. Status: ${currentBuild.currentResult}",
                        attachmentsPattern: "**/target/security-reports/*.html"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to AWS EC2 staging environment.'
                bat 'deploy-staging.bat'  // 假设 deploy-staging.bat 是部署脚本
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment.'
                bat 'run-integration-tests.bat'  // 假设 run-integration-tests.bat 是测试脚本
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to AWS EC2 production environment.'
                bat 'deploy-production.bat'  // 同样假设 deploy-production.bat 是部署脚本
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}
