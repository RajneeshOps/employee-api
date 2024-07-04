pipeline {
    agent any
    environment {
        SUDO_PASSWORD = credentials('rajops') // Store your sudo password securely in Jenkins credentials
    }
    stages {
        stage('Installation Go') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        // Update apt packages
                        sh "echo \$SUDO_PASSWORD | sudo -S apt update"
                        // Install Go using snap
                        sh "echo \$SUDO_PASSWORD | sudo -S snap install go --classic"
                    }
                }
            }
        }
        stage('Clone Repository') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        // Clone the Git repository
                        git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
                    }
                }
            }
        }
        stage('Testing') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        // Run go test and ignore errors
                        sh 'go test ./... || true'
                    }
                }
            }
        }
        stage('Generate HTML Report') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        // Run go test with coverage and generate HTML report
                        sh 'go test ./... -coverprofile=coverage.out || true'
                        sh 'go tool cover -html=coverage.out -o coverage.html || true'
                    }
                }
            }
        }
    }
}
