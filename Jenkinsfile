pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning source code'
                git branch: 'main', url: 'https://github.com/nguyen1405/nguyen1.git'
            }
        } // end Clone

        stage('Restore Package') {
            steps {
                echo 'Resolve dependencies'
                bat 'mvn dependency:resolve'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot project'
                bat 'mvn clean package'
            }
        }

        stage('Tests') {
            steps {
                echo 'Running tests...'
                bat 'mvn test'
            }
        }

        stage('Publish') {
            steps {
                echo 'Publishing...'
                bat 'mvn package -DskipTests -o ./target/publish'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
                bat '''
                    REM Chuyển file JAR lên server (thay user, server-ip, và đường dẫn)
                    scp ./target/publish/*.jar user@server-ip:/path/to/deploy/
                    REM Kết nối SSH và chạy ứng dụng (dừng app cũ nếu cần)
                    ssh user@server-ip "taskkill /IM java.exe /F || echo No running Java process & java -jar /path/to/deploy/*.jar &"
                '''
            }
        }
    } // end stages
} // end pipeline