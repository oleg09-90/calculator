pipeline {
    agent any
    
    environment {
        PATH = "/usr/bin:$PATH" // Путь к установленному Go
    }
    
    tools {
        go "Go" // Название инструмента Go, настроенного в Jenkins
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
}
