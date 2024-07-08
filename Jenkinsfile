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

    // Run ZAP Scan stage
    /*stage('Run ZAP Scan') {
        // Start ZAP and perform the scan
        sh "/var/lib/jenkins/workspace/'Scripted-Golang-DAST'/ZAP_2.14.0/zap.sh -cmd -port 8090 -quickurl http://34.66.129.93:8080/api/v1/employee/health -quickprogress -quickout ~/out2.html"
    }*/

    // Publish ZAP Scan Report stage
    stage('Publish ZAP Scan Report') {
        // Publish HTML report
        publishHTML(
            target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '/var/lib/jenkins/workspace/Scripted-Golang-DAST/ZAP_2.14.0/',
                reportFiles: 'out2.html',
                reportName: 'ZAP Scan Report',
                reportTitles: ''
            ]
        )
    }
}
