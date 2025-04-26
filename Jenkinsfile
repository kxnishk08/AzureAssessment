pipeline {
    agent any

    environment {
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\resources\\bin'
        PATH = "${DOCKER_PATH};${PATH}"

        DOCKERHUB_USERNAME = 'kxnishk2808'
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials-id-2808'   
        IMAGE_NAME = 'kanishkimg'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kxnishk08/AzureAssessment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKERHUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat "docker login -u %DOCKER_USER% -p %DOCKER_PASS%"
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                bat "docker push %DOCKERHUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG%"
            }
        }
    }

    post {
        success {
            echo 'Pushed Successfully'
        }
        failure {
            echo 'Push Failed'
        }
    }
}
