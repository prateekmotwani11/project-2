pipeline {
    agent any

    environment {
        IMAGE_NAME = "project-2-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        CONTAINER_NAME = "project-2-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prateekmotwani11/project-2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

	stage('Test Application') {
 	   steps {
               sh 'docker run --rm ${IMAGE_NAME}:${IMAGE_TAG} pytest test_app.py'
    	    }
	}	

        stage('Run Container') {
            steps {
                sh 'docker rm -f ${CONTAINER_NAME} || true'
                sh 'docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}:${IMAGE_TAG}'
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
