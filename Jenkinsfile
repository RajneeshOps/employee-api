node {
    def goHome = tool name: 'go', type: 'go'
    
    stage('Checkout') {
        git branch: 'main', url: 'https://github.com/RajneeshOps/Employee-API.git'
    }
    
    stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=golang-static-code-analysis -Dsonar.projectName='golang-static-code-analysis'"

    }
  }
}
