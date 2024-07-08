node {
    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
    }

    stage('Dependency Scan') {
        try {
            // Run your dependency scan step here
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: '',
                reportFiles: 'dep-check.html',
                reportName: 'Dependency Check Report'
            ])
        } catch (Exception e) {
            // Handle any exceptions here
            echo "Failed to publish HTML report: ${e.message}"
            currentBuild.result = 'FAILURE'
            error "Dependency scan failed"
        }
    }
}
