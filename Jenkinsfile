pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "abh-app"
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                bat 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe app.py'
                bat 'C:\\Users\\STUDENT\\AppData\\Local\\Microsoft\\WindowsApps\\python.exe'
            }
        }

        stage('3. Build & Tag Docker Image') {
            steps {
                script{
                DEF DOCKERpATH = 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'

                bat "\${dockerPath}\" --version"
                bat "\${dockerPath}\" build -t localhost:1111/job/2611P2/ -t localhost:1111/job/2611P2/:latest ."
                }
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                script {
                    def dockerPath = 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
                    bat "\${dockerPath}\" push -t localhost:1111/job/2611P2/"
                    bat "\${dockerPath}\" push -t localhost:1111/job/2611P2/:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Image ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} is available locally and in the registry."
        }
    }
}
