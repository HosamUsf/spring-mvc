pipeline {
    agent { label 'ahmedhakem' }
  
    environment {
        DOCKER_REGISTRY = 'your-docker-registry-url'
        IMAGE_NAME = 'mvnc'
        IMAGE_TAG = 'latest'  // You can replace this with a version or commit hash
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from your source repository
                git branch: 'main', url: 'https://github.com/ahmedabdelhakim13/spring-mvc.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    docker.build("${}:${latest}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Login to Docker registry
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-credentials-id') {
                        // Push the image to Docker registry
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Example deployment step (adjust for your environment)
                echo "Deploying the image ${IMAGE_NAME}:${IMAGE_TAG} to the environment..."
            }
        }
    }

    post {
        always {
            // Clean up after the build
            cleanWs()
        }
    }
}
