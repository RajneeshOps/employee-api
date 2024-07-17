node {
    // Environment variables
    def GIT_REPO = 'https://github.com/RajneeshOps/employee-api.git'
    def BRANCH = 'main'
    def SONAR_SCANNER = 'sonar'
    def GO_VERSION = 'Go'
    def ZAP_URL = 'https://github.com/zaproxy/zaproxy/releases/download/v2.14.0/ZAP_2.14.0_Linux.tar.gz'
    def ZAP_FOLDER = 'ZAP_2.14.0'
    def DEP_CHECK_REPORT = 'dep-check.html'
    def COVERAGE_PROFILE = 'coverage.out'
    def COVERAGE_HTML = 'coverage.html'
    def DAST_REPORT = 'out2.html'
    def GIT_CRED_ID = 'your-git-credentials-id'

    try {
        stage('Clone Repository') {
            // Clone the Git repository
            checkout([
                $class: 'GitSCM',
                branches: [[name: "*/${BRANCH}"]],
                extensions: [],
                userRemoteConfigs: [[
                    url: GIT_REPO,
                    credentialsId: GIT_CRED_ID
                ]]
            ])
        }
        
        stage('Code Compilation') {
            // Define the Go tool version
            def goHome = tool name: GO_VERSION, type: 'go'
            // Compile the Go code
            sh "${goHome}/bin/go build -o myapp main.go"
        }

        stage('Unit Testing') {
            // Run go test and ignore errors
            sh 'go test ./... || true'
        }

        stage('Bug-Analysis') {
            // Install and run GolangCI-lint for static code analysis
            sh 'go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest'
            env.PATH += ":$HOME/go/bin"
            sh 'golangci-lint run ./... || true'
        }

       
        stage('Dependency-Scan') {
            // Run OWASP Dependency-Check
            dependencyCheckPublisher(
                pattern: '**', 
                includesExcludes: [[includePattern: '**']], 
                failBuildOnCVSS: '10'
            )
        }

        stage('Generate HTML Report for Unit Test Coverage') {
            // Generate HTML Report for coverage
            sh 'go test ./... -coverprofile=${COVERAGE_PROFILE} || true'
            sh 'go tool cover -html=${COVERAGE_PROFILE} -o ${COVERAGE_HTML} || true'
        }

        

        stage('Publish Reports') {
            // Publish Dependency Check report
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '',
                reportFiles: DEP_CHECK_REPORT,
                reportName: 'Dependency Check Report'
            ])
            

            // Publish Unit Test Coverage report
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '',
                reportFiles: COVERAGE_HTML,
                reportName: 'Unit Test Coverage Report'
            ])
        }
    } catch (Exception e) {
        echo "Pipeline failed: ${e.message}"
        currentBuild.result = 'FAILURE'
        throw e
    }
}
