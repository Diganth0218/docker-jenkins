
pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        REGISTRY = 'localhost:5000'
        IMAGE_NAME = 'anil-demo-app'
    }

    stages {

        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                bat 'python --version'
                bat 'python -m py_compile app.py'
            }
        }

        stage('3. Build Docker Image') {
            steps {
                echo 'Checking Docker installation...'
                bat '"%DOCKER%" --version'

                echo 'Building Docker image...'
                bat '"%DOCKER%" build -t %REGISTRY%/%IMAGE_NAME%:%BUILD_NUMBER% -t %REGISTRY%/%IMAGE_NAME%:latest .'
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                echo 'Pushing Docker image...'
                bat '"%DOCKER%" push %REGISTRY%/%IMAGE_NAME%:%BUILD_NUMBER%'
                bat '"%DOCKER%" push %REGISTRY%/%IMAGE_NAME%:latest'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS! Docker image built and pushed!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}
