pipeline {
    agent any

    stages {
        stage('Check AWS Credentials') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-jenkins-credentials',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    bat '''
                        @echo off
                        echo Checking AWS credentials...

                        "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" sts get-caller-identity --region ap-south-1

                        if errorlevel 1 exit /b 1

                        echo AWS credentials are working!
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'AWS credentials test completed successfully!'
        }

        failure {
            echo 'AWS credentials test failed. Check Console Output.'
        }
    }
}
