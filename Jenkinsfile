pipeline {
    agent any
    tools {
        maven 'SonarQube' // Ensure this name matches the SonarQube Scanner configuration
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/name54321/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_8a9afa7d1fd6a8da0a3ed20d5ae60aab45927d35"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
