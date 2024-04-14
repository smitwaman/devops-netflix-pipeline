pipeline {
    agent any

    environment {
        // Define Docker image name
        DOCKER_IMAGE = 'snake-game:latest'
        DOCKER_REGISTRY = 'smitwaman/snake-game'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push Docker image to Docker registry
                script {
                    docker.withRegistry('https://${DOCKER_REGISTRY}', 'docker') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Build and Test') {
            steps {
                // Run Django tests inside Docker container
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'python manage.py test'
                    }
                }
            }
        }
        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv(credentialsId: 'snake-game') {
    // some block

                // Run SonarScanner
                sh '''
                    sonar-scanner \
                    -Dsonar.projectKey=snake-game \
                    -Dsonar.sources=src \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=${env.SONAR_TOKEN}
                '''
            }
        }
    }
        
    }
}
