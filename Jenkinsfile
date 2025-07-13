pipeline {
    agent any

    environment {
        IMAGE_NAME = "springboot-bankapp"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Clean workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rohan7351/springboot-bankapp.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat '.\\mvnw.cmd clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%DOCKER_TAG% ."
            }
        }

        // Uncomment below if you want to push to DockerHub
        // stage('Push Docker Image') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
        //             bat 'echo %PASSWORD% | docker login -u %USERNAME% --password-stdin'
        //             bat 'docker tag %IMAGE_NAME%:%DOCKER_TAG% %USERNAME%/%IMAGE_NAME%:%DOCKER_TAG%'
        //             bat 'docker push %USERNAME%/%IMAGE_NAME%:%DOCKER_TAG%'
        //         }
        //     }
        // }
    }
}
