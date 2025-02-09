pipeline {
    agent {
        docker {
            image 'python:3.9-slim'
            args '-p 8000:8000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                cd ./sources
                python -m venv venv
                . venv/bin/activate
                pip install pytest build
                python -m build
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                cd ./sources
                . venv/bin/activate
                pytest
                '''
                input message: 'Lanjut ke Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                sh './scripts/deploy.sh'
                sh 'sleep 60'  // Consider replacing with a proper health check
                sh './scripts/stop.sh'
            }
        }
    }
}


