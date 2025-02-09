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
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest tests/'
		input message: "Lanjut ke Deployment?"
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

