pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yash976-cmd/vikas-jenkin-test.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest
                '''

            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-ci-cd-app .'
            }
        }

        stage('Run Container') {
            steps {
            sh '''
            docker stop flask-ci-cd || true
            docker rm flask-ci-cd || true
            docker run -d --name flask-ci-cd -p 5000:5000 flask-ci-cd-app
            '''
            }
        }

    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Deployed successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
