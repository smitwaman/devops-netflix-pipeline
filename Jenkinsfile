pipeline {
    agent any

    environment {
        // Define environment variables
        DOCKER_IMAGE = 'snake-game:latest'
        DOCKER_REGISTRY = 'smitwaman/snake-game'
    }

    tools {
        // Define Git installation
        git 'Default'
        // Define Python installation
        jdk 'Python3' // Using JDK as a placeholder for Python
        
    }

    stages {
        stage('wsclean') {
            steps {
                // wsclean steps
                sh '''
                    # Add your wsclean commands here
                '''
            }
        }

        stage('Git Checkout') {
            steps {
                // Checkout code from Git repository
                checkout scm
            }
        }

        stage('Python venv build') {
            steps {
                // Create Python virtual environment and build
                sh '''
                    python3 -m venv myenv
                    source myenv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

    }
}
