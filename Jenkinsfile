pipeline {
    agent {
	docker {
            image 'python:3.9'
            args '--user root'
        }
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            
            steps {
                sh 'pip install pytest'
		sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
		input message : 'Lanjut ke tahap Deploy?'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') {
            
            steps {
                sh 'pip install pyinstaller'
		sh 'pyinstaller --onefile sources/add2vals.py'
            	sh 'sleep 60'
		
	    }
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
}

