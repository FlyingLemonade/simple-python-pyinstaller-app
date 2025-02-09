pipeline {
    agent {
	docker {
            image 'python:3.9'
            args '--user root'
        }
    }
    stages {
        stage('Build') {
            
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            
            steps {
                sh 'pip install pytest'
		sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
		
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
	stage ('Manual Approve'){
	    steps {
		input message : 'Lanjut ke tahap Deploy?'	 
	    }
	}
       stage('Deliver') {
            steps {
                sh 'pip install pyinstaller'
                sh 'pyinstaller --onefile sources/add2vals.py'
                sh 'mkdir -p ~/deployed_app'
                sh 'cp dist/add2vals ~/deployed_app/'
                sh 'chmod +x ~/deployed_app/add2vals'
                sh 'nohup ~/deployed_app/add2vals &'
                sh 'sleep 60'
                sh 'pkill -f add2vals'
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
}

