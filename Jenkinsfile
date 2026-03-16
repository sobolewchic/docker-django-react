pipeline {
    agent any
    
    environment {
        COMPOSE_PROJECT_NAME = "django-react"
    }

    stages {

        stage('Docker compose build') {
            steps {
                sh 'docker compose build --no-cache'
            }
        }

        stage('Start services') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Backend tests') {
            steps {
                sh 'docker compose exec -T backend pytest'
            }
        }

        stage('Stop services') {
            steps {
                sh 'docker compose down'
            }
        }
    }
}