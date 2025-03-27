pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Jithendra-Jithu/jenkins_with_docker2.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest tests/
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                mkdir -p build
                zip -r build/python-app.zip .
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/python-app.zip', fingerprint: true
            }
        }
    }
}
