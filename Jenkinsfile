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
                sh '/home/simple-python-pyinstaller-app/jenkins/scripts/test.sh'
	    }		
            
	    input { 
		message 'Lanjut ke Deployment'
	    }
            
        }
        stage('Deploy') { 
            steps {
                sh '/home/simple-python-pyinstaller-app' 
                sh 'sleep 60' 
                sh '/home/simple-python-pyinstaller-app/jenkins/scripts/kill.sh' 
            }
        }
    }
}
