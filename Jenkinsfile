pipeline {
    agent any

    tools{
        maven 'maven'
    }

    environment {
        COMPOSE_FILE = "docker-compose.yml"
         DOCKERHUB_USERNAME = 'ranjitha1024'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ranjitha1024/springboot-redis-demo-sak.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'rm -rf target || true'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t sak_redis_app .
                """
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh """
                if [ -f ${COMPOSE_FILE} ]; then
                    docker-compose -f ${COMPOSE_FILE} down || true
                fi
                """
            }
        }

        stage('Start New Containers') {
            steps {
                sh """
                docker-compose -f ${COMPOSE_FILE} up -d --build
                """
            }
        }
    }
     post {
        always {
            echo "Pipeline completed."
        }
        success {
            echo "Pipeline succeeded."
        }
        failure {
            echo "Pipeline failed."
        }
    }

}
