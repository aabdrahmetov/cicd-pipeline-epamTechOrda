pipeline {
    agent any
    stages {
        stage('Checkout Repository') {
            steps {
                echo 'Checking out the repository...'
                checkout scm
            }
        }
        stage('Build Application') {
            steps {
                echo 'Building the application...'
                sh 'chmod +x scripts/build.sh'
                sh './scripts/build.sh'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'chmod +x scripts/test.sh'
                sh './scripts/test.sh'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                script {
                    docker.build('aibabll/mybuildimage')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                echo 'Pushing the Docker image to the registry...'
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_aibabll') {
                        def app = docker.image('aibabll/mybuildimage')
                        app.push("${env.BUILD_NUMBER}")
                        app.push('latest')
                    }
                }
            }
        }
    }
}
