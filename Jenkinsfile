node {
    try {
        stage('Checkout') {
            // Checkout code from Git
            git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
        }

        stage('Dependency Scan') {
            // Run OWASP Dependency-Check
            def dependencyCheck = dependencyCheckPublisher pattern: '**'
            if (dependencyCheck > 0) {
                error "Dependency check found vulnerabilities"
            }
        }

        stage('Archive Report') {
            // Archive the dependency check report
            archiveArtifacts artifacts: '**/dep-check.html', allowEmptyArchive: true
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        // Clean up or finalize tasks if needed
    }
}
