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
                    # Create a virtual environment
                    python3 -m venv ${PYTHON_ENV}

                    # Activate the virtual environment
                    . ${PYTHON_ENV}/bin/activate

                    # Upgrade pip and install dependencies
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    # Activate virtual environment
                    . ${PYTHON_ENV}/bin/activate

                    # Run tests
                    pytest tests/
                '''
            }
        }

        stage('Build and Archive Artifacts') {
            steps {
                sh '''
                    # Activate virtual environment
                    . ${PYTHON_ENV}/bin/activate

                    # Build Python package
                    python setup.py sdist bdist_wheel
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


                
        
        
           
            
