pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "springboot-backend"
        FRONTEND_IMAGE = "springboot-frontend"
        BACKEND_PORT = "8084"
        FRONTEND_PORT = "8501"
        BACKEND_CONTAINER = "backend-container"
        FRONTEND_CONTAINER = "frontend-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/satyammaurya-cloud/Java-springboot-project.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                dir('backend') {
                    sh "docker build -t ${BACKEND_IMAGE} ."
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh "docker build -t ${FRONTEND_IMAGE} ."
                }
            }
        }

        stage('Remove Old Containers') {
            steps {
                sh """
                docker rm -f ${BACKEND_CONTAINER} || true
                docker rm -f ${FRONTEND_CONTAINER} || true
                """
            }
        }

        stage('Run Backend Container') {
            steps {
                sh """
                docker run -d --name ${BACKEND_CONTAINER} \
                -p ${BACKEND_PORT}:${BACKEND_PORT} \
                ${BACKEND_IMAGE}
                """
            }
        }

        stage('Run Frontend Container') {
            steps {
                sh """
                docker run -d --name ${FRONTEND_CONTAINER} \
                -p ${FRONTEND_PORT}:${FRONTEND_PORT} \
                ${FRONTEND_IMAGE}
                """
            }
        }
    }

    post {
        success {
            echo "Application Deployed Successfully 🚀"
        }
        failure {
            echo "Deployment Failed ❌"
        }
    }
}
