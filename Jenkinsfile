pipeline {
    agent {
        docker {
            image 'python:3.8-slim' // Specify the Docker image with Python 3.8
            args '-v /tmp:/tmp' // Optional: Additional arguments, such as mounting volumes
        }
    }

    environment {
        VENV_DIR = 'venv' // Define the virtual environment directory
    }

    stages {
        stage('Setup') {
            steps {
                echo 'Setting up the environment...'
                // Create a virtual environment
                sh 'python -m venv ${VENV_DIR}'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                // Activate the virtual environment and install dependencies
                sh '''
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }
//
//         stage('Run Tests') {
//             steps {
//                 echo 'Running tests...'
//                 // Activate the virtual environment and run tests
//                 sh '''
//                     . ${VENV_DIR}/bin/activate
//                     pytest
//                 '''
//             }
//         }

    }

    post {
        always {
            echo 'Cleaning up...'
            // Clean up virtual environment
            sh 'rm -rf ${VENV_DIR}'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}