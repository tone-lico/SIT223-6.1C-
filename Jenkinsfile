pipeline {
    agent any

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                // Replace Unix `sh` command with Windows `bat` command
                bat 'gradle clean build'
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                // Run tests using Windows batch command
                bat 'gradle test'
            }
            post {
                always {
                    // Email notification after tests
                    emailext subject: "Jenkins: Build #${env.BUILD_NUMBER} - Unit and Integration Tests",
                             body: "Build #${env.BUILD_NUMBER} completed the Unit and Integration Tests stage. Check Jenkins for details.",
                             to: 'developer@example.com',
                             attachLog: true
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                // Example using SonarQube
                bat 'sonar-scanner'
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                // Example using OWASP Dependency-Check (ensure the tool is installed and available in PATH)
                bat 'dependency-check.bat --project Jenkins --scan ./'
            }
            post {
                always {
                    // Email notification after the security scan
                    emailext subject: "Jenkins: Build #${env.BUILD_NUMBER} - Security Scan",
                             body: "Build #${env.BUILD_NUMBER} completed the Security Scan stage. Check Jenkins for details.",
                             to: 'developer@example.com',
                             attachLog: true
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                // Use Ansible or another tool compatible with Windows
                bat 'ansible-playbook deploy-staging.yml'
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                // Example using Postman Newman, ensure it's installed
                bat 'newman run integration_tests.postman_collection.json'
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                // Use AWS CLI for deployment (ensure AWS CLI is installed)
                bat 'aws s3 cp build-output.zip s3://your-production-bucket/'
            }
        }
    } // End of stages

} // End of pipeline
