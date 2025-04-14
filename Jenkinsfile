pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'Dockerhub-jenkins' // Jenkins credentials ID
        DOCKERHUB_REPO = 'jayparmar98/laravel-10-curd'
        IMAGE_TAG = '0.1' // You can replace this with a Git SHA or build number if needed
        //IMAGE = "laravel-10-App"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'develop', credentialsId: 'github', url: 'https://github.com/Jayparmar98/Laravel-10-Curd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def fullImageName = "${DOCKERHUB_REPO}:${IMAGE_TAG}"
                    echo "Building Docker image: ${fullImageName}"
                    bat "docker build -t ${fullImageName} ."
                }
            }
        }

         stage('Push to Docker Hub') {
            steps {
                script {
                    def fullImageName = "${DOCKERHUB_REPO}:${IMAGE_TAG}"
                    
                    echo "Logging into Docker Hub..."
                    withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CREDENTIALS}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        bat "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                    }

                    echo "Pushing image to Docker Hub..."
                    bat "docker push ${fullImageName}"
                }
            }
         }
    //     stage('Tag and Push to Local Registry') {
    //         steps {
    //             bat 'docker tag %IMAGE%:latest %REGISTRY%/%IMAGE%:latest'
    //             bat 'docker push %REGISTRY%/%IMAGE%:latest'
    //         }
    //     }

    //     stage('Deploy to Kubernetes') {
    //         steps {
    //             bat 'kubectl apply -f k8s\\deployment.yaml'
    //             bat 'kubectl apply -f k8s\\service.yaml'
    //             bat 'kubectl apply -f k8s\\configmap.yaml'
    //         }
    //     }
    // }

    // post {
    //     success {
    //         echo '✅ Deployment succeeded!'
    //     }
    //     failure {
    //         echo '❌ Deployment failed.'
    //     }
    }
}