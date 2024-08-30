pipeline {
    agent any

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                // Example for a Maven project
                sh 'mvn clean package'
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                // Run tests
                sh 'mvn test'
            }
            post {
                always {
                    // Email notification after tests
                    mail to: 'developer@example.com',
                         subject: "Jenkins: Build #${env.BUILD_NUMBER} - Unit and Integration Tests",
                         body: "Build #${env.BUILD_NUMBER} completed the Unit and Integration Tests stage. Check Jenkins for details.",
                         attachLog: true
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                // Example using SonarQube
                sh 'sonar-scanner'
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                // Example using OWASP Dependency-Check
                sh 'dependency-check.sh --project Jenkins --scan ./'
            }
            post {
                always {
                    // Email notification after the security scan
                    mail to: 'developer@example.com',
                         subject: "Jenkins: Build #${env.BUILD_NUMBER} - Security Scan",
                         body: "Build #${env.BUILD_NUMBER} completed the Security Scan stage. Check Jenkins for details.",
                         attachLog: true
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                // Example using Ansible
                sh 'ansible-playbook deploy-staging.yml'
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                // Example using Postman collection
                sh 'newman run integration_tests.postman_collection.json'
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                // Example using AWS CLI
                sh 'aws s3 cp build-output.zip s3://your-production-bucket/'
            }
        }
    } // End of stages

} // End of pipeline
