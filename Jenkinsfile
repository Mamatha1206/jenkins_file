pipeline {
    agent any

    environment {
        PYTHON_ENV = 'venv'  // Virtual environment name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Mamatha1206/jenkins_file.git'
            }
        }

        stage('Setup Virtual Environment & Install Dependencies') {
            steps {
                sh '''
                    # Ensure Python3 and venv are installed
                    sudo apt update && sudo apt install -y python3 python3-venv

                    # Create a virtual environment
                    python3 -m venv ${PYTHON_ENV}

                    # Activate the virtual environment
                    . ${PYTHON_ENV}/bin/activate

                    # Upgrade pip and install dependencies
                    ${PYTHON_ENV}/bin/pip install --upgrade pip
                    ${PYTHON_ENV}/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    # Run tests using virtual environment
                    ${PYTHON_ENV}/bin/python -m pytest tests/
                '''
            }
        }

        stage('Build and Archive') {
            steps {
                sh '''
                    # Build Python package using virtual environment
                    ${PYTHON_ENV}/bin/python setup.py sdist bdist_wheel
                '''
                
                # Archive artifacts
                archiveArtifacts artifacts: 'dist/*.whl', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build Completed Successfully!'
        }
        failure {
            echo '❌ Build Failed. Check logs for errors.'
        }
    }
}

        
                   
            
               
            
                
                
            


                
        
        
           
            
