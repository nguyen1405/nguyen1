pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                // Thêm lệnh triển khai (sẽ chi tiết ở bước 3)
                bat 'echo "Deploying to server..."'
            }
        }
    }
}
stage('Deploy') {
    steps {
        sh 'scp target/myapp.jar user@your-server-ip:/var/www/myapp/'
        sh 'ssh user@your-server-ip "java -jar /var/www/myapp/myapp.jar &"'
    }
}