node {

    stage('checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
    }

    stage('Install Dependencies') {
        sh 'go mod download'
    }

    stage('Run Snyk Scan') {
        // Install snyk CLI globally
        sh 'npm install -g snyk'
        
        // Run Snyk test across all projects
        sh 'snyk test --all-projects'
    }
}
