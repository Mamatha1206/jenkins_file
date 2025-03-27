pipeline {
    agent any

    environment {
        VENV = 'venv'  // Virtual environment name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Mamatha1206/jenkins_file.git'
                sh 'ls -la' // Check if files are pulled
            }
        }

        stage('Setup Python') {
            steps {
                sh 'which python3 || echo "Python3 not found!"'
                sh 'python3 --version'
                sh 'python3 -m venv $VENV || echo "venv creation failed!"'
                sh 'ls -la $VENV' // Check if venv is created
                sh 'source $VENV/bin/activate && pip install --upgrade pip || echo "Pip install failed!"'
                sh 'source $VENV/bin/activate && pip install -r requirements.txt || echo "Requirements installation failed!"'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'source $VENV/bin/activate && pytest tests/ || echo "Tests failed!"'
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'mkdir -p build && cp -r src build/'
                sh 'ls -la build/' // Check if build files are created
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}



        
                   
            
               
            
                
                
            


                
        
        
           
            
