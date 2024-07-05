node {
    // Define environment variables
    def SCANNER_HOME = tool name: 'sonar'
    def SONAR_HOST_URL = 'http://54.237.11.98:9000'
    def SONAR_PROJECT_KEY = 'golang-sca'
    def SONAR_TOKEN = 'sqp_ea5d795693f025cfd8cbc94f2b0a309b2f2c50e5'

    stage('SonarQube Analysis') {
        // Define SonarQube environment
        withSonarQubeEnv('sonar') {
            // Set JAVA_HOME to Java 17 path if not already set
            withEnv(['JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64', 'PATH+JAVA=${JAVA_HOME}/bin']) {
                // Run the SonarQube scanner
                sh """
                    ${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=${SONAR_HOST_URL} \
                    -Dsonar.login=${SONAR_TOKEN} || exit 1
                """
            }
        }
    }
}
