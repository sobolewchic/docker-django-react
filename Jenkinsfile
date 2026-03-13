pipeline {
    agent any
    
    options {
        skipDefaultCheckout()
    }
    environment {
        COMPOSE_PROJECT_NAME = "django-react"
    }

    stages {

        stage('Clean workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/sobolewchic/docker-django-react.git',
                    credentialsId: 'c2012d75-5da8-4890-8da0-3c36b53e7388', // ID 
                    branch: 'main'
                )
            }
        }

        stage('Docker compose build') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Start services') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Backend tests') {
            steps {
                sh 'docker compose exec -T django pytest || true'
            }
        }

        stage('Stop services') {
            steps {
                sh 'docker compose down'
            }
        }
    }
}