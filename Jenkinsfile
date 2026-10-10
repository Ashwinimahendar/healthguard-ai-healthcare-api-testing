pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Node and npm') {
            steps {
                bat 'node --version'
                bat 'npm --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Run Healthcare API Tests') {
            steps {
                bat 'if not exist reports mkdir reports'
                bat 'npx newman run Healthcare-API.postman_collection.json -e Healthcare.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export reports/healthcare-api-report.html'
            }
        }
    }

    post {
        always {
            archiveArtifacts(
                artifacts: 'reports/*.html',
                allowEmptyArchive: true
            )
        }
    }
}