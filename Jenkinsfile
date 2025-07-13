pipeline {
    agent any

    environment {
        IMAGE_NAME = "springboot-bankapp"
        DOCKER_TAG = "latest"
        SONARQUBE_SERVER = 'SonarQube' // must match name configured in Jenkins > Configure System
    }

    tools {
        maven 'Maven 3.8.8' // replace with your installed Maven name if different
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
                bat './mvnw clean package -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    bat './mvnw sonar:sonar -Dsonar.projectKey=springboot-bankapp'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%DOCKER_TAG% ."
            }
        }
    }
}
