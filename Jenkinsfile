// pipeline {
//     agent any

//     stages {
//         stage('Clone') {
//             steps {
//                 echo 'Cloning source code'
//                 git branch: 'main', url: 'https://github.com/nguyen1405/nguyen1.git'
//             }
//         } // end Clone

//         stage('Restore Package') {
//             steps {
//                 echo 'Resolve dependencies'
//                 bat 'mvn dependency:resolve'
//             }
//         }

//         stage('Build') {
//             steps {
//                 echo 'Building Spring Boot project'
//                 bat 'mvn clean package'
//             }
//         }

//         stage('Tests') {
//             steps {
//                 echo 'Running tests...'
//                 bat 'mvn test'
//             }
//         }

//        stage('Publish') {
//     steps {
//         echo 'Publishing...'
//         bat 'mvn package -DskipTests'
//         bat 'mkdir publish || echo Directory already exists'
//         bat 'move target\\demo2-0.0.1-SNAPSHOT.jar publish\\'
//     }
// }

//      stage('Deploy') {
//     steps {
//         echo 'Deploying to server...'
//         bat '''
//             scp publish\\demo2-0.0.1-SNAPSHOT.jar admin@192.168.1.100:/home/admin/app/ || exit /b 1
//             ssh admin@192.168.1.100 "taskkill /IM java.exe /F || echo No running Java process & java -jar /home/admin/app/demo2-0.0.1-SNAPSHOT.jar &" || exit /b 1
//         '''
//     }
// }
//     } // end stages
// } // end pipeline