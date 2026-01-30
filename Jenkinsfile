pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python3 --version
                python3 -m venv venv
                source venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest
                '''
            }
        }

        stage('Build & Package') {
            steps {
                sh '''
                zip -r hello-devops-build.zip app.py requirements.txt
                '''
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'hello-devops-build.zip', fingerprint: true
            }
        }
    }
}
