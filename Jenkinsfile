pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package' // Xây dựng ứng dụng
            }
        }
        stage('Deploy') {
            steps {
                // Thêm lệnh triển khai (sẽ chi tiết ở bước 3)
                sh 'echo "Deploying to server..."'
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