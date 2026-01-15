// pipeline {
//     agent any

//     tools {
//         nodejs 'NodeJS-22'
//     }

//     stages {
//         stage('Clone Code') {
//             steps {
//                 git branch: 'main',
//                     url: 'https://github.com/KarthikP47/demodevop.git'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 bat 'npm install'
//             }
//         }

//         stage('Build React App') {
//             steps {
//                 bat 'npm run build'
//             }
//         }
//     }

//     post {
//         success {
//             echo 'React build successful 🎉'
//         }
//         failure {
//             echo 'Build failed ❌'
//         }
//     }
// }
pipeline {
    agent any

    environment {
        IMAGE_NAME = "<none>"
        CONTAINER_NAME = "awesome_northcutt"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/KarthikP47/demodevop.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker run -d -p 5173:5173 --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo 'React app deployed using Docker successfully 🎉'
        }
        failure {
            echo 'Deployment failed ❌'
        }
    }
}