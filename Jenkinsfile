pipeline {
    agent any  // The pipeline can run on any available agent (node)

    environment {
        // Define the image name and the Docker Hub repository
        IMAGE_NAME = "my-web-app"
        DOCKER_HUB_REPO = "nikhita27/labfinal"
    }

    stages {
        // Stage 1: Checkout the code from Git repository
        stage('Checkout') {
            steps {
                // Checkout the latest code from the repository
                git 'https://github.com/NikhitaK27/lab.git'
            }
        }

        // Stage 2: Build Docker Image
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repository
                    docker.build("$DOCKER_HUB_REPO")
                }
            }
        }

        // Stage 3: Run Tests (optional)
        stage('Run Tests') {
            steps {
                script {
                    // Run tests inside the Docker container (optional)
                    docker.image("$DOCKER_HUB_REPO").inside {
                        echo 'Running tests inside the Docker container...'
                        // Here, you can add any tests that you want to run inside the container
                        // For example: `sh 'curl -f http://localhost:8080/healthcheck'`
                    }
                }
            }
        }

        // Stage 4: Push Docker Image to Docker Hub
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the built image to Docker Hub or any Docker registry
                    docker.withRegistry('', 'docker-hub-credentials') {
                        docker.image("$DOCKER_HUB_REPO").push('latest')  // Push the latest tag
                    }
                }
            }
        }
    }

    post {
        // Actions to take after the build completes, whether successful or failed
        always {
            // Clean up, remove any leftover Docker containers or images
            echo 'Cleaning up Docker images and containers'
            sh 'docker system prune -f'
        }
    }
}
