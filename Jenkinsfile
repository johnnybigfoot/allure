node {

        stage('Checkout') {
            checkout scm
            sh "git pull origin master"
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
                    allure includeProperties: false, jdk: '', results: [[path: 'build/allure-results']]

                }
            }



}

