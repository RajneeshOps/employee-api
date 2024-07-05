node {
    def goHome = tool name: 'go', type: 'go'

    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/Employee-API.git'
    }

    stage('SonarQube Analysis') {
        def scannerHome = tool name: 'SonarQube', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        withSonarQubeEnv('SonarQube') { // Ensure 'SonarQube' matches the name configured in Jenkins
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=golang-static-code-analysis -Dsonar.projectName='golang-static-code-analysis'"
        }
    }
}
