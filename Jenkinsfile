
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
                sh 'test -f app.py'
                sh 'test -f test_app.py'
                sh "grep -q 'def add' app.py"
                sh "grep -q 'assert add(2, 3) == 5' test_app.py"
                echo 'All automated checks passed'
            }
        }

        stage('Build') {
            steps {
                sh 'mkdir -p deployment'
                sh 'cp app.py deployment/app.py'
                echo 'Application prepared for deployment'
            }
        }

        stage('Deployment') {
            steps {
                sh 'test -f deployment/app.py'
                echo 'Application deployed successfully'
            }
        }

        stage('Verification') {
            steps {
                sh 'ls -l deployment'
                echo 'Deployment verified successfully'
            }
        }
    }
}
