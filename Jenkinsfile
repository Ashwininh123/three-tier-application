pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'GitHub repository connected successfully!'
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

        stage('Verify Docker Image') {
            steps {
                sh 'docker images'
                echo 'Docker image build completed successfully!'
            }
        }

        stage('Success') {
            steps {
                echo 'Three-tier application pipeline completed successfully!'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Pipeline completed!'
        }

        failure {
            echo 'FAILED: Please check the Console Output.'
        }
    }
}
