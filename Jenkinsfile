pipeline {
    agent any

    tools {
        maven 'maven'   // Must match Jenkins Maven installation name
    }

    environment {
        DEPLOY_DIR = "/opt/deploy/redis-demo"
    }

    stages {

        stage("Clone Repository") {
            steps {
                dir(DEPLOY_DIR) {
                    git branch: 'main', url: 'https://github.com/Ranjitha1024/springboot-redis-demo-sak.git'
                }
            }
        }

        stage("Build JAR") {
            steps {
                dir(DEPLOY_DIR) {
                    sh "mvn clean package -DskipTests"
                }
            }
        }

        stage("Docker Compose Down") {
            steps {
                dir(DEPLOY_DIR) {
                    sh "docker compose down || true"
                }
            }
        }

        stage("Docker Build") {
            steps {
                dir(DEPLOY_DIR) {
                    sh "docker compose build --no-cache"
                }
            }
        }

        stage("Docker Deploy") {
            steps {
                dir(DEPLOY_DIR) {
                    sh "docker compose up -d"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment Successful 🎉 App running at: http://65.2.171.164:8084"
        }
        failure {
            echo "Deployment Failed ❌ Please check console logs."
        }
    }
}
