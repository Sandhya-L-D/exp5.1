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
            string(
                credentialsId: 'dockerhub_credentials',
                variable: 'DOCKER_PASS'
            )
        ]) {
            withEnv([
                "PATH+DOCKER=C:/Users/Sandhya L D/AppData/Local/Programs/DockerDesktop/resources/bin"
            ]) {
                bat '''
                    echo %DOCKER_PASS% | docker login --username sandhyald --password-stdin
                    if errorlevel 1 exit /b 1

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

