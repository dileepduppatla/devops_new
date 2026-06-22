pipeline {
    agent any
 
    environment {
        IMAGE_NAME = "hello-app"
        CONTAINER_NAME = "hello-container"
    }
 
    stages {
 
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/dileepduppatla/devops_new'
            }
        }
 
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
 
        stage('Test') {
            steps {
                sh 'python3 hello.py'
            }
        }
 
        stage('Stop Old Container') {
            steps {
                script {
                    sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                    '''
                }
            }
        }
 
        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
 
    }
}
