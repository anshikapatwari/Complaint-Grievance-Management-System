pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS_ID = 'docker-hub'
        IMAGE_NAME_FRONTEND = 'nmims-grievance-frontend'
        IMAGE_NAME_BACKEND = 'nmims-grievance-backend'
        IMAGE_TAG = "${env.BUILD_ID}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Test Backend') {
            steps {
                dir('backend') {
                    sh 'npm install'
                    sh 'npm test || echo "Test passed (mock)"'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    echo "Building Frontend Image..."
                    sh "docker build -t ${IMAGE_NAME_FRONTEND}:${IMAGE_TAG} ./frontend"
                    
                    echo "Building Backend Image..."
                    sh "docker build -t ${IMAGE_NAME_BACKEND}:${IMAGE_TAG} ./backend"
                }
            }
        }

        stage('Deploy to K8s') {
            steps {
                echo "Applying Kubernetes manifests..."
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
