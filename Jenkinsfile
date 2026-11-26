
pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"
    }

    stages {

        stage('1. Checkout Code') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                echo 'Checking Python application...'
                bat 'python --version'
                bat 'python -m py_compile app.py'
                echo 'Python application validation successful!'
            }
        }

        stage('3. Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker --version'
                bat 'docker build -t %REGISTRY%/%IMAGE_NAME%:%BUILD_NUMBER% -t %REGISTRY%/%IMAGE_NAME%:latest .'
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                echo 'Pushing Docker image...'
                bat 'docker push %REGISTRY%/%IMAGE_NAME%:%BUILD_NUMBER%'
                bat 'docker push %REGISTRY%/%IMAGE_NAME%:latest'
            }
        }

    }

    post {
        success {
            echo 'SUCCESS: Jenkins pipeline completed!'
            echo 'Docker image built and pushed successfully.'
        }

        failure {
            echo 'ERROR: Jenkins pipeline failed. Check the console output.'
        }

        always {
            echo 'Jenkins pipeline execution finished.'
        }
    }
}
