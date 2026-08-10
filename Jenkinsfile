pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Obtendo o código'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t cepel-energy-api:1.2 .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop cepel-api || true
                    docker rm cepel-api || true
                    docker run -d \
                      --name cepel-api \
                      -p 8000:8000 \
                      cepel-energy-api:1.2
                '''
            }
        }

        stage('Health Check') {
    steps {
        sh 'curl --fail --retry 10 --retry-delay 2 --retry-all-errors http://localhost:8000/health'

            }
        }
    }
}
