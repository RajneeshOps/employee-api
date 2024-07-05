node {
    stage('SonarQube Analysis') {
        // Define SonarQube environment
        withSonarQubeEnv('sonar') {
            // Run the SonarQube scanner
            sh "${SCANNER_HOME}/bin/sonar || exit 1"
        }
    }
}
