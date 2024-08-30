pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Use a build automation tool like Maven or Gradle
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Specify testing tools like JUnit for unit tests and Postman/Newman for integration tests
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Use a tool like SonarQube for code analysis
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Use a security scanning tool like OWASP ZAP or Snyk
                sh 'snyk test'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Environment...'
                // Deploy the application to a staging server, e.g., AWS EC2
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy/'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Re-run integration tests on the staging environment
                sh 'curl -X GET http://staging-server/api/health'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
                // Deploy the application to the production server
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy/'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded!'
            emailext(
                subject: "Jenkins Pipeline Success",
                body: "The Jenkins pipeline has completed successfully.",
                to: "testsnapetest@gmail.com"
            )
        }
        failure {
            echo 'Pipeline failed!'
            emailext(
                subject: "Jenkins Pipeline Failure",
                body: "The Jenkins pipeline has failed.",
                to: "testsnapetest@gmail.com"
            )
        }
    }
}
