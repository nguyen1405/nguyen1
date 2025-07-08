pipeline {
    agent any
    environment {
        DEPLOY_SERVER = 'admin@192.168.1.100'
        DEPLOY_PATH = 'C:\\home\\admin\\app'
    }
    stages {
        stage('Checkout') {
            steps {
                // Lấy mã nguồn từ Git
                bat 'git clone https://github.com/nguyen1405/nguyen1.git'
            }
        }
        stage('Build') {
            steps {
                // Biên dịch và đóng gói dự án
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // Chạy các bài kiểm thử
                bat 'mvn test'
            }
        }
        stage('Publish') {
            steps {
                // Di chuyển JAR đã đóng gói
                bat 'mkdir publish'
                bat 'move target\\*.jar publish\\'
                bat 'chmod +x publish\\*.jar'
                bat 'echo Artifact published to publish directory'
            }
        }
        stage('Deploy') {
            steps {
                // Triển khai lên máy chủ từ xa
                sshagent(['508b67c5-9f01-4d4c-af85-e1e7388af8e8']) {
                    bat 'pscp publish\\*.jar %DEPLOY_SERVER%:%DEPLOY_PATH%\\'
                    bat 'plink %DEPLOY_SERVER% "taskkill /IM java.exe /F || echo No running process"'
                    bat 'plink %DEPLOY_SERVER% "start java -jar %DEPLOY_PATH%\\*.jar"'
                }
                bat 'echo Deployment completed'
            }
        }
    }
    post {
        success {
            bat 'echo Pipeline succeeded! Application deployed.'
        }
        failure {
            bat 'echo Pipeline failed. Check the logs for details.'
        }
    }
}