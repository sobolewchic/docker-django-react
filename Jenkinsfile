pipeline {

    agent any


    environment {

        REGISTRY = "192.168.126.128:8082"

        BACKEND_IMAGE = "${REGISTRY}/backend"

        FRONTEND_IMAGE = "${REGISTRY}/frontend"

        TAG = "${BUILD_NUMBER}"

    }


    stages {


        stage('Checkout') {

            steps {

                git branch: 'main',
                url: 'https://github.com/sobolewchic/docker-django-react.git'

            }

        }


        stage('Docker Login') {

            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'nexus',
                        usernameVariable: 'USER',
                        passwordVariable: 'PASS'
                    )
                ]) {

                    sh '''

                    echo $PASS | docker login ${REGISTRY} \
                    -u $USER \
                    --password-stdin

                    '''

                }

            }

        }


        stage('Build Backend') {

            steps {

                sh '''

                docker build \
                -t ${BACKEND_IMAGE}:${TAG} \
                ./backend

                '''

            }

        }


        stage('Build Frontend') {

            steps {

                sh '''

                docker build \
                -t ${FRONTEND_IMAGE}:${TAG} \
                ./frontend

                '''

            }

        }



        stage('Push Images') {

            steps {

                sh '''

                docker push ${BACKEND_IMAGE}:${TAG}

                docker push ${FRONTEND_IMAGE}:${TAG}

                '''

            }

        }



        stage('Deploy Helm') {

            steps {

                sh '''

                helm upgrade --install library ./helm \
                --set backend.image.tag=${TAG} \
                --set frontend.image.tag=${TAG}


                kubectl rollout status deployment/backend

                kubectl rollout status deployment/frontend

                '''

            }

        }

    }


}
