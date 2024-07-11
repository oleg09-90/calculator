pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-go-app' // Имя Docker-образа
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    sh 'go mod download' // Скачиваем зависимости Go
                    sh 'go test ./...'   // Запускаем тесты Go
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE) // Строим Docker-образ
                }
            }
        }

        stage('Deploy Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.example.com', 'docker_credentials_id') {
                        docker.image(env.DOCKER_IMAGE).push() // Загружаем Docker-образ в Docker Registry
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build successful! Deploying...'
            // Дополнительные действия при успешной сборке
        }
        failure {
            echo 'Build failed!'
            // Дополнительные действия при ошибке сборки
        }
    }
}
