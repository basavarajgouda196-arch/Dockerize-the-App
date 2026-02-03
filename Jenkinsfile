pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/basavarajgouda196-arch/Dockerize-the-App.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-python-app:latest .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'hub',
                    usernameVariable: 'basavarajgouda',
                    passwordVariable: 'MT6vCUJBibcVTOHMM8lwHk7RelM'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "basavarajgouda" --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                    docker tag my-python-app:latest $DOCKER_USER/my-python-app:latest
                    docker push $DOCKER_USER/my-python-app:latest
                '''
            }
        }
    }
}
