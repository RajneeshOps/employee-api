node {
  stage('SCM') {
    checkout([
      $class: 'GitSCM',
      branches: [[name: '*/main']],
      extensions: [],
      userRemoteConfigs: [[
        url: 'https://github.com/RajneeshOps/attendance-api.git'
      ]]
    ])
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
