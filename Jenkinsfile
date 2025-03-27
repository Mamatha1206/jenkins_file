pipeline {
    agent any

    environment {
        PYTHON_ENV = "${WORKSPACE}/venv"  // Absolute path to avoid activation issues
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
                    sudo apt update && sudo apt install -y python3 python3-venv python3-pip

                    # Remove any existing virtual environment
                    rm -rf ${PYTHON_ENV}

                    # Create a new virtual environment
                    python3 -m venv ${PYTHON_ENV}

                    # Upgrade pip inside the virtual environment
                    ${PYTHON_ENV}/bin/pip install --upgrade pip

                    # Install dependencies from requirements.txt
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
                    # Build Python package inside the virtual environment
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

        
                   
            
               
            
                
                
            


                
        
        
           
            
