pipeline {
    agent any

    environment {
        VENV = 'venv'  // Virtual environment name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Mamatha1206/jenkins_file.git'
            }
        }

        stage('Setup Python') {
            steps {
                sh 'python3 -m venv $VENV'
                sh 'source $VENV/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'source $VENV/bin/activate && pytest tests/'
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'mkdir -p build && cp -r src build/'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}


        
                   
            
               
            
                
                
            


                
        
        
           
            
