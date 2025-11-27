pipeline {
    agent any

    tools {
        jdk 'Java17'
        maven 'maven'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ranjitha1024/springboot-redis-demo-sak.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Compose Down') {
            steps {
                sh '''
                echo "Stopping existing containers..."
                docker-compose down || true
                '''
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                echo "Building docker images..."
                docker-compose build --no-cache
                '''
            }
        }

        stage('Deploy Containers') {
            steps {
                sh '''
                echo "Starting application using Docker Compose..."
                docker-compose up -d
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful! Application is live at http://13.126.188.155:8084"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
