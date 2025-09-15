pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('jk-dh-pat')
}
    stages {
        stage('Clonning Git Repository') {
            steps {
                git branch: 'main', credentialsId: 'jk-gh-pat', url: 'https://github.com/opsthinkdev/jk-private-gh-orx.git'
            }
        }
    stage('Building Docker Image') {
            steps {
                sh 'docker build -t opsthinkdev/webapp:$BUILD_NUMBER .'
            }
        }
    stage('Login to Docker Hub') {
           steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
    stage('Push Image') {
           steps {
                sh 'docker push opsthinkdev/webapp:$BUILD_NUMBER'
            }
        }
    stage('Deploy Application') {
            steps {
                sh 'docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}'
            }
        }    
    }
}
