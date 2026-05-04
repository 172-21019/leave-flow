pipeline {
    agent any

    environment {
        IMAGE_NAME = 'leave-manager'
        IMAGE_TAG  = "v${BUILD_NUMBER}"
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        CONTAINER_NAME = 'leave-manager-app'
        APP_PORT = '3000'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Cloning repository...'
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                echo '📦 Installing dependencies...'
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                echo '🧪 Running unit tests...'
                sh 'npm test'
            }
        }
        stage('Code Quality') {
            steps {
                echo '🔍 Running audit...'
                sh 'npm audit --audit-level=high || true'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "🐳 Building Docker image: ${IMAGE_NAME}:${IMAGE_TAG}"
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest"
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo '🚀 Pushing to DockerHub...'
                sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }
        stage('Deploy') {
            steps {
                echo '🚢 Deploying...'
                sh """
                    docker stop ${CONTAINER_NAME} || true
                    docker rm   ${CONTAINER_NAME} || true
                    docker run -d \
                        --name ${CONTAINER_NAME} \
                        -p ${APP_PORT}:3000 \
                        --restart unless-stopped \
                        ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
        stage('Health Check') {
            steps {
                echo '❤️ Verifying health...'
                sh 'sleep 5'
                sh "curl -f http://localhost:${APP_PORT}/health || exit 1"
            }
        }
    }

    post {
        success { echo '✅ Leave Manager deployed successfully!' }
        failure { echo '❌ Pipeline failed! Check logs.' }
        always  { sh 'docker image prune -f || true' }
    }
}
