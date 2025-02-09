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
                sh ''
            }
        }
        stage('Test') {
            steps {
                sh 'pytest tests/'
            }
        }
        stage('Deploy') { 
            steps {
                sh './scripts/deploy.sh' 
                input message: 'Sudah selesai menggunakan Python App? (Klik Proceed untuk mengakhiri)' 
                sh './scripts/stop.sh' 
            }
        }
    }
}

