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