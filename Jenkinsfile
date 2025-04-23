pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abhishek-khodke/twitter-sentiment-analysis-python-ML.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t twitter-sentiment-model .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    docker push abhishekkhodke/twitter-sentiment-model:latest
                    docker logout
                    """
                }
            }
        }
    }
}
