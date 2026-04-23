pipeline {
    agent any

    environment {
        IMAGE = "Dhoni-dubey-portfolio1"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Code pulled automatically"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 80:80 $IMAGE:latest'
            }
        }
    }
}
