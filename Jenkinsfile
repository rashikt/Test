pipeline {
    agent any

    environment {
        // Define the Python version and virtual environment directory
        PYTHON_VERSION = '3.8'
        VENV_DIR = 'venv'
    }

    stages {
        stage('Setup') {
            steps {
                echo 'Setting up the environment...'
                // Install the specified Python version if not already available
                sh '''
                    if ! command -v python${PYTHON_VERSION} &>/dev/null; then
                        sudo apt-get update
                        sudo apt-get install -y python${PYTHON_VERSION}
                    fi
                '''
                // Create a virtual environment
                sh "python${PYTHON_VERSION} -m venv ${VENV_DIR}"
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
    }

    post {
        always {
            echo 'Cleaning up...'
            // Clean up virtual environment
            sh "rm -rf ${VENV_DIR}"
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}