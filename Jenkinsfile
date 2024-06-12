pipeline {
    agent {
        docker {
            image 'python:3.8-slim'
            args '-v /tmp:/tmp'
        }
    }

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Setup') {
            steps {
                script {
                    echo 'Setting up the environment...'
                    // Create a virtual environment
                    sh 'python -m venv ${VENV_DIR}'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    // Activate the virtual environment and install dependencies
                    sh '''
                        . ${VENV_DIR}/bin/activate
                        pip install --upgrade pip
                        pip install -r requirements.txt
                    '''
                }
            }
        }
//
//         stage('Run Tests') {
//             steps {
//                 script {
//                     echo 'Running tests...'
//                     // Activate the virtual environment and run tests
//                     sh '''
//                         . ${VENV_DIR}/bin/activate
//                         pytest
//                     '''
//                 }
//             }
//         }
//
//         stage('Package') {
//             steps {
//                 script {
//                     echo 'Packaging application...'
//                     // Package the application if necessary
//                     sh '''
//                         . ${VENV_DIR}/bin/activate
//                         python setup.py sdist bdist_wheel
//                     '''
//                 }
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