pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Mamatha1206/jenkins_file.git'
            }
        }
        stage('Setup Virtual Environment & Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest tests/
                '''
            }
        }
        stage('Build and Archive') {
            steps {
                sh '''
                    . venv/bin/activate
                    python setup.py sdist bdist_wheel
                '''
                archiveArtifacts artifacts: 'dist/*.whl', fingerprint: true
            }
        }
    }
}

                
        
        
           
            
