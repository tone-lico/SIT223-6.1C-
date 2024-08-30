pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                sh 'snyk test'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Environment...'
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy/'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'curl -X GET http://staging-server/api/health'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
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
