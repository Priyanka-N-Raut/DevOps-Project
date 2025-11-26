pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "priyanka4316/devops-app"
        CREDENTIALS_ID = "docker-hub-creds"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Priyanka-N-Raut/DevOps-Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${DOCKER_HUB_REPO}:latest .
                """
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    """
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${DOCKER_HUB_REPO}:latest"
            }
        }

        stage('Deploy Container') {
            steps {
                sh """
                docker rm -f devops-app || true
                docker run -d -p 9090:80 --name devops-app ${DOCKER_HUB_REPO}:latest
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs."
        }
    }
}
