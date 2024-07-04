
node {
  stage('Installation Go') {
      try {
          // Update apt packages
          sh 'sudo apt update'
          // Install Go using snap
          sh 'sudo snap install go --classic'
      } catch (Exception e) {
          echo "Failed to install Go: ${e.message}"
          currentBuild.result = 'FAILURE'
          error("Failed to install Go")
      }
  }
  
  stage('Clone Repository') {
      try {
          // Clone the Git repository
          git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
      } catch (Exception e) {
          echo "Failed to clone repository: ${e.message}"
          currentBuild.result = 'FAILURE'
          error("Failed to clone repository")
      }
  }
  
  stage('Testing') {
      try {
          // Run go test and ignore errors
          sh 'go test ./... || true'
      } catch (Exception e) {
          echo "Failed to run tests: ${e.message}"
          currentBuild.result = 'FAILURE'
          error("Failed to run tests")
      }
  }
  
  stage('Generate HTML Report') {
      try {
          // Run gotest with specify the output format and generate HTML Report
          sh 'go test ./... -coverprofile=coverage.out || true'
          sh 'go tool cover -html=coverage.out -o coverage.html || true'
      } catch (Exception e) {
          echo "Failed to generate HTML report: ${e.message}"
          currentBuild.result = 'FAILURE'
          error("Failed to generate HTML report")
      }
  }
}
