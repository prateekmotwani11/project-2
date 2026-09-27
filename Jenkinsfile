pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prateekmotwani11/project-2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t project-2-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f project-2-container || true'
                sh 'docker run -d --name project-2-container -p 5000:5000 project-2-app:latest'
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 5'
                sh 'curl -f http://localhost:5000/health'
            }
        }
    }
}
