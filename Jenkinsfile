pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Ankit-MS24/Basic_test.git'
            }
        }

        stage('Setup Python') {
            steps {
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'venv\\Scripts\\activate && pytest --junitxml=report.xml'
            }
        }

        stage('Publish Report') {
            steps {
                junit 'report.xml'
            }
        }
    }
}
