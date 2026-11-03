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
                bat 'dir /a'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('application-code/app-tier') {
                    bat 'docker build -t three-tier-app:latest .'
                }
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat 'docker images'
                echo 'Docker image build completed successfully!'
            }
        }

        stage('Deploy to App EC2') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'app-ec2-ssh',
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_USER'
                    ),
                    usernamePassword(
                        credentialsId: 'aws-jenkins-credentials',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    bat '''
                        @echo off

                        docker save -o three-tier-app.tar three-tier-app:latest
                        if errorlevel 1 exit /b 1

                        powershell -NoProfile -ExecutionPolicy Bypass -Command "$p=Start-Process -FilePath 'C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe' -ArgumentList 'ec2-instance-connect open-tunnel --instance-connect-endpoint-id eice-072a44e3c63b04ef6 --instance-id i-02434948c1819a3dd --remote-port 22 --local-port 2222' -PassThru -WindowStyle Hidden; $p.Id | Set-Content tunnel.pid; $ready=$false; for ($i=0; $i -lt 30; $i++) { if (Test-NetConnection 127.0.0.1 -Port 2222 -InformationLevel Quiet) { $ready=$true; break }; Start-Sleep -Seconds 2 }; if (-not $ready) { throw 'Tunnel did not open' }"

                        if errorlevel 1 exit /b 1

                        scp -i "%SSH_KEY%" -P 2222 -o StrictHostKeyChecking=no -o UserKnownHostsFile=NUL three-tier-app.tar %SSH_USER%@localhost:/home/ec2-user/

                        if errorlevel 1 exit /b 1

                        ssh -i "%SSH_KEY%" -p 2222 -o StrictHostKeyChecking=no -o UserKnownHostsFile=NUL %SSH_USER%@localhost "sudo docker load -i /home/ec2-user/three-tier-app.tar && (sudo docker stop three-tier-backend || true) && (sudo docker rm three-tier-backend || true) && sudo docker run -d --name three-tier-backend --restart unless-stopped -p 4000:4000 --env-file /home/ec2-user/app-tier/.env three-tier-app:latest && sleep 5 && curl -fsS http://localhost:4000/health"

                        if errorlevel 1 exit /b 1

                        echo Deployment completed successfully!
                    '''
                }
            }
        }
    }

    post {
        always {
            bat '''
                @echo off
                powershell -NoProfile -Command "if (Test-Path tunnel.pid) { Stop-Process -Id (Get-Content tunnel.pid) -Force -ErrorAction SilentlyContinue; Remove-Item tunnel.pid -Force }"
            '''
        }

        success {
            echo 'SUCCESS: Pipeline and deployment completed!'
        }

        failure {
            echo 'FAILED: Please check Console Output.'
        }
    }
}
