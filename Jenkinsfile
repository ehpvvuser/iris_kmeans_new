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
        withCredentials([string(credentialsId: 'ghcr_pat', variable: 'GH_PAT')]) {
            bat 'echo %GH_PAT% | docker login ghcr.io -u ehpvvuser --password-stdin'
        }
    }
}


        stage('Build Docker Image') {
            steps {
                bat 'docker build -t  %IMAGE_NAME% .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push  %IMAGE_NAME% .'
            }
        }
    }
}
