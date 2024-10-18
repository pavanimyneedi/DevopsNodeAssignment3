pipeline {
    agent any
    
    environment {
        REGISTRY = 'myregistry'              // Replace with your Docker registry (e.g., Docker Hub or cloud registry)
        REGISTRY_CREDENTIALS = 'dockerhub'   // Jenkins credential ID for Docker registry login
        IMAGE = 'myapp'                      // Name of your Docker image
        TAG = 'latest'                       // Tag for your Docker image
    }
    
    stages {
        
        stage('Pull Code') {
            steps {
                // Pull code from Git repository
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build Docker image from the Dockerfile in the repository
                    sh 'docker build -t ${REGISTRY}/${IMAGE}:${TAG} .'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run unit tests (adjust command based on your testing framework)
                    sh 'npm test'
                }
            }
        }
        
        stage('Push Image to Registry') {
            steps {
                script {
                    // Log in to the Docker registry
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin ${REGISTRY}'
                    
                    // Tag and push the Docker image to the registry
                    sh 'docker tag ${REGISTRY}/${IMAGE}:${TAG} ${REGISTRY}/${IMAGE}:${TAG}'
                    sh 'docker push ${REGISTRY}/${IMAGE}:${TAG}'
                }
            }
        }
        
        stage('Deploy to Cloud') {
            steps {
                script {
                    // Deploy Docker container to cloud infrastructure (e.g., AWS ECS, Azure ACI, or GCP GKE)
                    // This depends on the cloud service you're using
                    // Example for Docker Compose deployment:
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
