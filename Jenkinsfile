pipeline{
    agent any 
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Mamatha1206/jenkins_file.git', branch:'main'
            }
        }
        stage('Set Up Virtual Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate' 
            }
        }
        stage('Install Dependencies') {
            steps {
                 sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && PYTHONPATH=$PWD pytest test/'
            }
        }
        stage('Build Artifact') {
            steps {
                sh '. venv/bin/activate && python setup.py sdist'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}


        
                   
            
               
            
                
                
            


                
        
        
           
            
