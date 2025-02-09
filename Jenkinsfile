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
                python -m pip install pytest
                python -m build
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'pytest ./sources'
                input message: 'Lanjut ke Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                sh './scripts/deploy.sh'
                sh 'sleep 60'  
                sh './scripts/stop.sh'
            }
        }
    }
}

