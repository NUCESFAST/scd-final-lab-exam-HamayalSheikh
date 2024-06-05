pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id') // Replace with your Jenkins credentials ID for Docker Hub
        GITHUB_CREDENTIALS = credentials('github-credentials-id') // Replace with your Jenkins credentials ID for GitHub
        ROLL_NUMBER = '1125'
    }

    stages {
        stage('Checkout_1125') {
            steps {
                script {
                    echo 'Checking out code from GitHub...'
                    git credentialsId: "${env.GITHUB_CREDENTIALS}", url: 'https://github.com/your-github-username/your-repo.git' // Replace with your repo URL
                }
            }
        }

        stage('Install_Dependencies_1125') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    dir('backend') {
                        sh 'npm install'
                    }
                    dir('frontend') {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Build_Backend_Image_1125') {
            steps {
                script {
                    echo 'Building Docker image for backend...'
                    dir('backend') {
                        sh 'docker build -t your-dockerhub-username/backend:latest .'
                    }
                }
            }
        }

        stage('Build_Frontend_Image_1125') {
            steps {
                script {
                    echo 'Building Docker image for frontend...'
                    dir('frontend') {
                        sh 'docker build -t your-dockerhub-username/frontend:latest .'
                    }
                }
            }
        }

        stage('Push_Backend_Image_1125') {
            steps {
                script {
                    echo 'Pushing Docker image for backend to Docker Hub...'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push your-dockerhub-username/backend:latest'
                }
            }
        }

        stage('Push_Frontend_Image_1125') {
            steps {
                script {
                    echo 'Pushing Docker image for frontend to Docker Hub...'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push your-dockerhub-username/frontend:latest'
                }
            }
        }

        stage('Deploy_and_Validate_1125') {
            steps {
                script {
                    echo 'Deploying and validating the application...'
                    // Here you could run docker-compose up or kubectl apply commands to deploy the application
                    // Then run tests or checks to validate the deployment
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Cleaning up...'
                sh 'docker system prune -f'
            }
        }
        success {
            script {
                echo 'Pipeline completed successfully.'
            }
        }
        failure {
            script {
                echo 'Pipeline failed.'
            }
        }
    }
}
