pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the Node.js application...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Building Docker image...'
                script {
                    docker.build("my-node-app:${env.BUILD_ID}")
                }
                echo 'Deploying Docker container...'
                script {
                    docker.withRegistry('https://registry.example.com', 'credentials-id') {
                        docker.image("my-node-app:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }
}
