
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        
stage('Install Dependencies') {
    steps {
        bat '"C:/Users/vidhy/AppData/Local/Python/pythoncore-3.14-64/python.exe" -m pip install -r requirements.txt'
    }
}

stage('Run Tests') {
    steps {
        bat '"C:/Users/vidhy/AppData/Local/Python/pythoncore-3.14-64/python.exe" -m pytest test_app.py -v'
    }
}


        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jenkins-docker-demo .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker rm -f jenkins-demo-container || exit /b 0'
                bat 'docker run -d --name jenkins-demo-container -p 5000:5000 jenkins-docker-demo'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Completed Successfully!'
        }
        failure {
            echo 'CI/CD Pipeline Failed!'
        }
    }
}
