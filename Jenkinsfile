pipeline {
    agent any

    environment {
        IMAGE = "dhoni-dubey-portfolio1"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Code pulled automatically by Jenkins"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }

        stage('Load Image to Kind') {
            steps {
                sh 'kind load docker-image $IMAGE:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'helm upgrade --install portfolio ~/Cluster/apache-chart'
            }
        }
    }
}
