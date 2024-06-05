pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        GITHUB_CREDENTIALS = credentials('github-credentials-id')
        KUBECONFIG_CREDENTIALS = credentials('kubeconfig-credentials-id') // Add your Kubernetes credentials ID
        ROLL_NUMBER = '1125'
    }

    stages {
        stage('Checkout_1125') {
            steps {
                script {
                    echo 'Checking out code from GitHub...'
                    git credentialsId: "${env.GITHUB_CREDENTIALS}", url: 'https://github.com/your-github-username/your-repo.git'
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

        stage('Deploy_to_Kubernetes_1125') {
            steps {
                script {
                    echo 'Deploying to Kubernetes...'
                    withCredentials([file(credentialsId: 'kubeconfig-credentials-id', variable: 'KUBECONFIG')]) {
                        sh 'kubectl apply -f backend-deployment-1125.yaml'
                        sh 'kubectl apply -f frontend-deployment-1125.yaml'
                        sh 'kubectl apply -f mongodb-deployment-1125.yaml'
                    }
                }
            }
        }

        stage('Scale_and_Test_1125') {
            steps {
                script {
                    echo 'Scaling and testing the deployment...'
                    sh 'kubectl scale deployment backend-deployment-1125 --replicas=5'
                    sh 'kubectl scale deployment frontend-deployment-1125 --replicas=5'
                    // Add any additional test commands here
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
