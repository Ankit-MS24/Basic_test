pipeline {
    agent any

    environment {
        PYTHON_VERSION = "3.10"
        VENV_DIR = "venv"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Ankit-MS24/Basic_test.git'
            }
        }

        stage('Set Up Python Virtual Environment') {
            steps {
                bat "python -m venv %VENV_DIR%"
                bat "call %VENV_DIR%\\Scripts\\activate && python --version"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat "call %VENV_DIR%\\Scripts\\activate && pip install pytest"
            }
        }

        stage('Run Pytest') {
            steps {
                bat "call %VENV_DIR%\\Scripts\\activate && pytest test_example.py --junitxml=reports/test-results.xml"
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'reports/test-results.xml'
            }
        }

        stage('Cleanup') {
            steps {
                bat "rmdir /s /q %VENV_DIR%"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/test-results.xml', fingerprint: true
        }
        success {
            echo 'Tests Passed ✅'
        }
        failure {
            echo 'Tests Failed ❌'
        }
    }
}
