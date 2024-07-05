node {
    def goHome = tool name: 'go', type: 'go'

    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/Employee-API.git'
    }

    stage('SonarQube Analysis') {
        def scannerHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        withSonarQubeEnv('SonarQube Scanner') { // Ensure 'SonarQube' matches the name configured in Jenkins
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=golang-static-code-analysis -Dsonar.projectName='golang-static-code-analysis'"
        }
    }
}
