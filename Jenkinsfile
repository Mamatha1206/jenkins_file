pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Mamatha1206/jenkins_file.git'
            }
        }
        stage('Install Dependencies & Run Tests') {
            steps {
                sh '''
                    pip install -r requirements.txt
                    pytest tests/
                '''
            }
        }
        stage('Build and Archive') {
            steps {
                sh 'python setup.py sdist bdist_wheel'
                archiveArtifacts artifacts: 'dist/*.whl', fingerprint: true
            }
        }
    }
}
