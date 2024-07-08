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

        stage('Publish Dependency Check Report') {
    // Publish Dependency Check report
    publishHTML([
        allowMissing: false,
        alwaysLinkToLastBuild: false,
        keepAll: true,
        reportDir: '',
        reportFiles: 'dep-check.html',
        reportName: 'Dependency Check Report'
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
