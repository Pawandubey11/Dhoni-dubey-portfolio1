pipeline {
    agent any

    environment {
        IMAGE = "dhoni-dubey-portfolio1"
        CHART_PATH = "/home/ubuntu/Cluster/apache-chart"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Code pulled automatically by Jenkins"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE:latest .
                docker images
                '''
            }
        }

        stage('Load Image to Kind') {
            steps {
                sh '''
                kind load docker-image $IMAGE:latest
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                helm upgrade --install portfolio $CHART_PATH
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                kubectl get pods
                kubectl get svc
                '''
            }
        }
    }
}
