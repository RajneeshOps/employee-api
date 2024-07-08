node {
    try {
        stage('Checkout') {
            // Checkout code from Git
            git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
        }

        stage('Dependency Scan') {
            // Run OWASP Dependency-Check
            dependencyCheckPublisher(pattern: '**', includesExcludes: [[includePattern: '**']], failBuildOnCVSS: '10')
        }

        stage('Archive Report') {
            // Archive the dependency check report
            archiveArtifacts(artifacts: '**/dependency-check-report.xml', allowEmptyArchive: true)
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
