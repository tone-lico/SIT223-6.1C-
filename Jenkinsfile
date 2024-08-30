pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Use a build tool like Maven or Gradle
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Use a testing tool like JUnit or TestNG
                // sh 'mvn test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/test-results/**/*.xml', allowEmptyArchive: true
                    script {
                        def testStatus = currentBuild.currentResult
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Test Stage: ${testStatus}",
                             body: "The test stage has completed with status: ${testStatus}.",
                             attachLog: true
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Use a code analysis tool like SonarQube
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Use a security scanning tool like OWASP ZAP or Snyk
                // sh 'snyk test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/security-reports/**/*.xml', allowEmptyArchive: true
                    script {
                        def securityStatus = currentBuild.currentResult
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Security Scan Stage: ${securityStatus}",
                             body: "The security scan stage has completed with status: ${securityStatus}.",
                             attachLog: true
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Deploy to staging server, e.g., AWS EC2
                // sh 'deploy to staging script'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Run integration tests on staging environment
                // sh 'run staging tests script'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Deploy to production server, e.g., AWS EC2
                // sh 'deploy to production script'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
    }
}