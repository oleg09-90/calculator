pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Шаг клонирования репозитория
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Шаг сборки и тестирования проекта на Go
                sh '''
                if [ ! -f go.mod ]; then
                    go mod init github.com/oleg09-90/calculator
                fi
                go mod tidy
                go test .
                '''
            }
        }
    }
}
