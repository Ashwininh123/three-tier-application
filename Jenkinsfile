pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'GitHub repository connected successfully!'
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                echo 'Validating application files...'
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('application-code/app-tier') {
                    sh 'docker build -t three-tier-app:latest .'
                }
            }
        }

        stage('Success') {
            steps {
                echo 'Three-tier application Docker image built successfully!'
            }
        }
    }
}
