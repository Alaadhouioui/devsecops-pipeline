pipeline {
    agent any

    environment {
        // Replace with your Jenkins SonarQube installation name
        SONARQUBE_SERVER = 'SonarQube' 
        
        // Replace with your Snyk token stored in Jenkins credentials
        SNYK_TOKEN = credentials('snyk-token') 
    }

    stages {
        stage('Checkout') {
            steps {
                // Replace with your GitHub repository URL and branch
                git url: 'https://github.com/your-username/your-repo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Example: Maven build, change if using another build system
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Static Code Analysis - SonarQube') {
            steps {
                script {
                    // Make sure SONARQUBE_SERVER matches your Jenkins SonarQube config
                    withSonarQubeEnv("${SONARQUBE_SERVER}") {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }

        stage('Dependency Scanning - Snyk') {
            steps {
                // Authenticates Snyk using token stored in Jenkins
                sh 'snyk auth ${SNYK_TOKEN}'
                
                // Run vulnerability test
                sh 'snyk test'
                
                // Optional: upload project snapshot to Snyk dashboard
                sh 'snyk monitor' 
            }
        }

        stage('Python Security Scan - Bandit') {
            steps {
                // Recursively scan current directory for Python security issues
                sh 'bandit -r . -lll'
            }
        }

        stage('Container Scan - Trivy') {
            steps {
                // Scan local filesystem or container images for vulnerabilities
                sh 'trivy fs .' 
                // To scan a remote Docker image, replace with:
                // sh 'trivy image your-docker-image:tag'
            }
        }

        stage('Dependency Check - OWASP') {
            steps {
                // Replace "MyProject" with your project name
                // Output will be in reports/dependency-check.html
                sh 'dependency-check --project "MyProject" --scan . --format HTML --out reports/dependency-check.html'
            }
        }

        stage('Tests') {
            steps {
                echo 'Running tests...'
                // Replace with your test command if not using Maven
                sh 'mvn test' 
            }
        }
    }

    post {
        always {
            // Archive all HTML reports for viewing in Jenkins
            archiveArtifacts artifacts: 'reports/**/*.html', allowEmptyArchive: true
            
            // Archive JUnit test results (adjust path for your project)
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs!'
        }
    }
}
