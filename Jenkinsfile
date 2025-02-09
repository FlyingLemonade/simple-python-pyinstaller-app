pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh '/home/simple-python-pyinstaller-app/scripts/test.sh'
            }
        }
        stage('Deploy') { 
            steps {
                sh '/home/simple-python-pyinstaller-app/scripts/deliver.sh' 
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
                sh '/home/simple-python-pyinstaller-app/scripts/kill.sh' 
            }
        }
    }
}




