node {
    try {
        stage('Checkout') {
            checkout scm
            sh "git checkout $Branch"
            sh "git pull"
        }

            stage('Clean') {
                sh "chmod +x gradlew"
                sh "./gradlew clean --no-daemon"
            }

            stage('Test') {
                echo "Run tests"

                try {
                    sh "./gradlew clean test --info --no-daemon"
                } finally {
                    publishHTML(target: [
                            allowMissing         : false,
                            alwaysLinkToLastBuild: true,
                            keepAll              : true,
                            reportDir            : './build/reports/tests/test',
                            reportFiles          : 'index.html',
                            reportName           : "CRMT Test Report"
                    ])
                }
            }



        } catch (e) {
        currentBuild.result = "FAILED"
    }
}
