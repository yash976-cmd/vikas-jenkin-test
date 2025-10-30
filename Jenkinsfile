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
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-jenkins-demo:latest")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 flask-jenkins-demo:latest'
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
