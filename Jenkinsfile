pipeline {
    agent any

    environment {
        IMAGE = "dhoni-dubey-portfolio1"
        TAG = "latest"
        CHART_PATH = "/home/ubuntu/Cluster/apache-helm"
        RELEASE_NAME = "portfolio"
        NAMESPACE = "default"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                set -e
                docker build -t $IMAGE:$TAG .
                docker images | grep $IMAGE
                '''
            }
        }

        stage('Load Image to Kind') {
            steps {
                sh '''
                set -e
                kind load docker-image $IMAGE:$TAG
                '''
            }
        }

        stage('Deploy to Kubernetes using Helm') {
            steps {
                sh '''
                set -e
                helm upgrade --install $RELEASE_NAME $CHART_PATH \
                  --namespace $NAMESPACE \
                  --create-namespace \
                  --set image.repository=$IMAGE \
                  --set image.tag=$TAG \
                  --wait --timeout 120s
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                kubectl rollout status deployment/$RELEASE_NAME -n $NAMESPACE
                kubectl get pods -n $NAMESPACE
                kubectl get svc -n $NAMESPACE
                '''
            }
        }
    }
}
