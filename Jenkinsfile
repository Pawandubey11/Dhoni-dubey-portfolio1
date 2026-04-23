
pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo "Code already cloned by Jenkins"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t pawanportfolio:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 80:80 pawanportfolio:latest'
            }
        }
    }
}
