pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Automated Testing') {
            steps {
                sh 'python -m pip install pytest'
                sh 'python -m pytest -v'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t devops-test-app .'
            }
        }
        stage('Deployment') {
            steps {
                sh 'docker rm -f devops-test-container || true'
                sh 'docker run -d --name devops-test-container devops-test-app'
            }
        }
        stage('Verification') {
            steps {
                sh 'docker logs devops-test-container'
            }
        }
    }
}
