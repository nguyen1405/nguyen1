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
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Publish') {
            steps {
                bat 'if not exist publish mkdir publish'
                bat 'move target\\*.jar publish\\'
                bat 'if exist publish\\*.jar (chmod +x publish\\*.jar) else (echo No JAR file found)'
                bat 'echo Artifact published to publish directory'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['your-ssh-credential-id']) {
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