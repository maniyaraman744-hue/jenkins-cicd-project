
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'test -f application/index.html'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh "grep -q 'Welcome to My DevOps Project' application/index.html"
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop myapp || true
                    docker rm myapp || true
                    docker run -d \
                      --name myapp \
                      -p 80:80 \
                      myapp:latest
                '''
            }
        }
    }
}
