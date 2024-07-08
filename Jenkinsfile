node {
stage('Checkout') {
    git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git/'
}

stage('Dependency Scan') {
    publishHTML([
        allowMissing: false,
        alwaysLinkToLastBuild: false,
        keepAll: true,
        reportDir: '',
        reportFiles: 'dep-check.html',
        reportName: 'Dependency Check Report'
    ])
}
