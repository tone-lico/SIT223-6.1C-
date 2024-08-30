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
