node {
    def SNYK_TOKEN = credentials('snyk1')

    stage('checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
    }

    stage('Install Dependencies') {
        sh 'go mod download'
    }

    stage('Run Snyk Scan') {
        // Use Snyk plugin step to run security tests
        snykSecurityScan credentialsId: 'snyk1', failOnIssues: true
    }
}
