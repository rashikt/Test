pipeline {
    agent any

    environment {
        VENV_DIR = 'venv' // Define the virtual environment directory
    }

    stages {
        stage('Setup') {
              steps {
                echo 'Setting up the environment...'
                // Update package list and install dependencies
                sh '''
                    apt-get update
                    command -v python3.8 || apt-get install -y python3.8 python3.8-venv
                '''
                // Create a virtual environment
                sh 'python3.8 -m venv ${VENV_DIR}'
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
//
//         stage('Package') {
//             steps {
//                 echo 'Packaging application...'
//                 // Package the application if necessary
//                 sh '''
//                     . ${VENV_DIR}/bin/activate
//                     python setup.py sdist bdist_wheel
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