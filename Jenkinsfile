pipeline {
    agent any
   environment {
    DOCKER_IMAGE = 'sandhyald/exp5mca'
    DOCKER_CREDENTIALS = 'dockerhub_credentials'
}
    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sandhya-L-D/exp5.1.git'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                bat 'dir'
            }
        }
stage('Docker Test') {
    steps {
        echo 'Testing Docker from Jenkins...'

        bat 'whoami'

        bat 'dir "C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe"'

        bat '"C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" --version'

        bat '"C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" info'
    }
}
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub_credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %DOCKER_IMAGE%:latest'
                    bat 'docker logout'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }
    }
}

