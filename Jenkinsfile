node {
    // Define parameters
    def stagesToRun = params.STAGES_TO_RUN.split(',').collect { it.trim() }
    def goToolName = params.GO_TOOL_NAME
    def scannerToolName = params.SCANNER_TOOL_NAME
    def dependencyToolName = params.DEPENDENCY_TOOL_NAME
    def gitBranch = params.GIT_BRANCH
    def gitCredentialsId = params.GIT_CREDENTIALS_ID
    def gitUrl = params.GIT_URL
    def sonarQubeEnvName = params.SONARQUBE_ENV_NAME

    // Define tools
    def goHome = tool name: goToolName, type: 'Go'
    def scannerHome = tool name: scannerToolName, type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    def dependencyCheckHome = tool name: dependencyToolName, type: 'org.jenkinsci.plugins.DependencyCheck.DependencyCheckInstallation'

    try {
        if (stagesToRun.contains('Checkout')) {
            stage('Checkout') {
                echo "Running Checkout stage"
                checkout([$class: 'GitSCM', branches: [[name: gitBranch]], doGenerateSubmoduleConfigurations: false, extensions: [], userRemoteConfigs: [[credentialsId: gitCredentialsId, url: gitUrl]]])
            }
        }

        if (stagesToRun.contains('Build')) {
            stage('Build') {
                echo "Running Build stage"
                withEnv(["PATH+GO=${goHome}/bin"]) {
                    sh '''
                    go mod tidy
                    go mod download
                    go build -o employee-api .
                    '''
                }
            }
        }

        if (stagesToRun.contains('Unit Test')) {
            stage('Unit Test') {
                echo "Running Unit Test stage"
                withEnv(["PATH+GO=${goHome}/bin"]) {
                    sh 'go test ./... -v | tee unit-test-results.xml'
                }
            }
        }

        if (stagesToRun.contains('SonarQube Analysis')) {
            stage('SonarQube Analysis') {
                echo "Running SonarQube Analysis stage"
                withSonarQubeEnv(sonarQubeEnvName) {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

        if (stagesToRun.contains('Dependency Scan')) {
            stage('Dependency Scan') {
                echo "Running Dependency Scan stage"
                dependencyCheck additionalArguments: '--scan . --format ALL', odcInstallation: dependencyToolName
            }
        }

        if (stagesToRun.contains('Archive Report')) {
            stage('Archive Report') {
                echo "Running Archive Report stage"
                archiveArtifacts artifacts: 'unit-test-results.xml', allowEmptyArchive: true

                echo "Publishing Reports"
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'dependency-check-report.html',
                    reportName: 'Dependency Check Report',
                    reportTitles: ''
                ])
            }
        }

    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        echo "Build failed with exception: ${e}"
        throw e
    } finally {
        if (currentBuild.result == 'SUCCESS') {
            echo 'Build successful!'
        } else {
            echo 'Build failed!'
        }
    }
}
