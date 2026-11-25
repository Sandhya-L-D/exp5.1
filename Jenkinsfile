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
        withEnv(["PATH+DOCKER=C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin"]) {
            echo 'Testing Docker...'
            bat 'whoami'
            bat 'where docker'
            bat 'docker --version'
            bat 'docker info'
        }
    }
}
        stage('Build Docker Image') {
    steps {
        withEnv(["PATH+DOCKER=C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin"]) {
            bat 'docker build -t sandhyald/exp5mca:latest .'
        }
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
            withEnv([
                "PATH+DOCKER=C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin"
            ]) {
                bat '''
                    powershell.exe -NoProfile -NonInteractive -Command "$env:DOCKER_PASS | docker login --username $env:DOCKER_USER --password-stdin; if ($LASTEXITCODE -ne 0) { exit $LASTEXITCODE }"

                    docker push sandhyald/exp5mca:latest
                '''
            }
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

