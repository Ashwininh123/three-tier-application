pipeline {
    agent any

    stages {
        stage('Test EC2 Tunnel') {
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
                        echo Testing EC2 Instance Connect tunnel...

                        "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" ec2-instance-connect open-tunnel --instance-connect-endpoint-id eice-072a44e3c63b04ef6 --instance-id i-02434948c1819a3dd --remote-port 22 --local-port 2222 --region ap-south-1
                    '''
                }
            }
        }
    }
}
