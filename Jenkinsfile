pipeline {
    agent any

    environment {
        IMAGE_NAME = "ghcr.io/ehpvvuser/iris_kmeans_newpipe:latest"
        GH_USER = "ehpvvuser"
        GH_PAT = credentials('ghcr_pat') // Jenkins credential ID for GitHub token
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ehpvvuser/iris_kmeans_new.git'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $GH_PAT | docker login ghcr.io -u $GH_USER --password-stdin'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}
