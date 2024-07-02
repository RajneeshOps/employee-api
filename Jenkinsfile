node {
    // Define the Go tool version
    def goHome = tool name: 'go', type: 'go'

    stage('Checkout') {
        // Checkout the code from the Git repository
        git branch: 'main', url: 'https://github.com/RajneeshOps/employee-api.git'
    }
    
    stage('Code Compilation') {
        // Compile the Go code
        sh "${goHome}/bin/go build -o myapp main.go" 
    }
}