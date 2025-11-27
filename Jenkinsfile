pipeline {
    agent any

    tools {
        maven 'maven'  // Make sure this matches the Maven installation name in Jenkins
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
                sh 'docker-compose down || true'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build --no-cache'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful! Application is live at http://35.154.102.39:8084"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
