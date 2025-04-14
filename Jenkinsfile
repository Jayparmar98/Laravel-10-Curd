pipeline {
    agent any

    environment {
        IMAGE = "laravel-10-App"
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
                    def imageName = "laravel-10-app"
                    def imageTag = "1.0"
                    def fullImageName = "${imageName}:${imageTag}"

                    echo "Building Docker image: ${fullImageName}"

                    // Build the Docker image
                    bat "docker build -t ${fullImageName} ."
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