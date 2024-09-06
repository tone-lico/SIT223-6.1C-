pipeline {
    agent any


    environment {
        EMAIL_RECIPIENT = 'testsnapetest@gmail.com'
    }


    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                echo 'Tools that can be used in this stage:'
                echo '1. Maven: mvn clean package'
                echo '2. Gradle: gradle build'
                echo '3. npm: npm install'
                // sh 'mvn clean package'
            }
        }


        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'Tools that can be used in this stage:'
                echo '1. JUnit: mvn test'
                echo '2. TestNG: mvn test'
                echo '3. Mocha/Chai (for Node.js): npm test'
                // sh 'mvn test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/test-results/**/*.xml', allowEmptyArchive: true
                    script {
                        def logContent = currentBuild.rawBuild.getLog(100).join('\n')
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Test Stage: ${currentBuild.currentResult}",
                             body: "The test stage has completed with status: ${currentBuild.currentResult}.\n\nLogs:\n${logContent}"
                    }
                }
            }
        }


        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                echo 'Tools that can be used in this stage:'
                echo '1. SonarQube: sonar-scanner'
                echo '2. ESLint (for JavaScript/Node.js): eslint .'
                echo '3. Checkstyle (for Java): mvn checkstyle:check'
                // sh 'sonar-scanner'
            }
        }


        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                echo 'Tools that can be used in this stage:'
                echo '1. OWASP ZAP: zap-cli start'
                echo '2. Snyk: snyk test'
                echo '3. Dependency Check: dependency-check.sh --project MyProject'
                // sh 'snyk test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/security-reports/**/*.xml', allowEmptyArchive: true
                    script {
                        def logContent = currentBuild.rawBuild.getLog(100).join('\n')
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Security Scan Stage: ${currentBuild.currentResult}",
                             body: "The security scan stage has completed with status: ${currentBuild.currentResult}.\n\nLogs:\n${logContent}"
                    }
                }
            }
        }


        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'Tools that can be used in this stage:'
                echo '1. AWS CLI: aws s3 cp target/myapp.jar s3://my-staging-bucket/'
                echo '2. Kubernetes (for containerized apps): kubectl apply -f deployment.yaml'
                echo '3. Ansible: ansible-playbook -i inventory deploy.yml'
                // sh 'deploy to staging script'
            }
        }


        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'Tools that can be used in this stage:'
                echo '1. Postman/Newman: newman run postman_collection.json'
                echo '2. Selenium: mvn verify'
                echo '3. Cypress (for frontend testing): cypress run'
                // sh 'run staging tests script'
            }
        }


        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'Tools that can be used in this stage:'
                echo '1. AWS CLI: aws s3 cp target/myapp.jar s3://my-production-bucket/'
                echo '2. Kubernetes: kubectl apply -f production-deployment.yaml'
                echo '3. Jenkins Deploy Plugin (for automated deployments): deploy target/myapp.jar'
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



