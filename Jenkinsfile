pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-web-app"
        DOCKER_HUB_REPO = "nikhita27/labfinal"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/NikhitaK27/lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Use the correct credential ID: '1Nikhita'
                    docker.withRegistry('https://index.docker.io/v1/', '1Nikhita') {
                        docker.build("$DOCKER_HUB_REPO")
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    docker.image("$DOCKER_HUB_REPO").inside {
                        echo 'Running tests'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Use the correct credential ID: '1Nikhita'
                    docker.withRegistry('https://index.docker.io/v1/', '1Nikhita') {
                        docker.image("$DOCKER_HUB_REPO").push('latest')
                    }
                }
            }
        }
    }
}

