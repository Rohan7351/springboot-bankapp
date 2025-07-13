pipeline {
    agent any

    environment {
        IMAGE_NAME = "springboot-bankapp"
        DOCKER_TAG = "latest"
        SONARQUBE_SERVER = 'SonarQube'  // Must match the name configured in Jenkins > Manage Jenkins > Configure System
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
                    bat './mvnw clean verify sonar:sonar -Dsonar.projectKey=springboot-bankapp -Dsonar.token=%SONAR_TOKEN% -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml'
                }
            }
        }


        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%DOCKER_TAG% .'
            }
        }
    }
}
