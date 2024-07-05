node {
  stage('Installation Pre-Requisites') {
      try {
          // Install GolangCI-lint
          sh 'go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest'
          // Add $HOME/go/bin to PATH
          env.PATH += ":$HOME/go/bin"
      } catch (Exception e) {
          echo "Error occurred during installation pre-requisites: ${e.getMessage()}"
      }
  }

  stage('Clone Repository') {
      try {
          // Clone the Git repository
          git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
      } catch (Exception e) {
          echo "Error occurred during repository cloning: ${e.getMessage()}"
      }
  }

  stage('Linting') {
      try {
          // Run golangci-lint and ignore errors
          sh 'golangci-lint run ./... || true'
      } catch (Exception e) {
          echo "Error occurred during linting: ${e.getMessage()}"
      }
  }

  stage('Generate HTML Report') {
      try {
          // Run golangci-lint with the --out-format option to specify the output format
          sh 'golangci-lint run ./... --out-format html > report.html || true'
      } catch (Exception e) {
          echo "Error occurred during HTML report generation: ${e.getMessage()}"
      }
  }
}
