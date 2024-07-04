node {
    // Environment variables
    def TARGET_URL = 'https://github.com/RajneeshOps/employee-api.git'

    // Checkout stage
    stage('Checkout') {
        checkout scmGit(
            branches: [[name: '*/main']],
            extensions: [],
            userRemoteConfigs: [[url: TARGET_URL]]
        )
    }

    // Install ZAP stage
    stage('Install ZAP') {
        // Download and install OWASP ZAP
        sh 'wget https://github.com/zaproxy/zaproxy/releases/download/v2.14.0/ZAP_2.14.0_Linux.tar.gz'
        sh 'tar -xvf ZAP_2.14.0_Linux.tar.gz'
    }

   
    // Publish ZAP Scan Report stage
    stage('Publish ZAP Scan Report') {
        // Publish HTML report
        publishHTML(
            target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '/var/lib/jenkins/workspace/Declarative Pipeline GoLang DAST/ZAP_2.14.0/',
                reportFiles: 'out2.html',
                reportName: 'ZAP Scan Report',
                reportTitles: ''
            ]
        )
    }
}
