pipeline {
    agent any

    environment {
        JMETER_HOME = 'C:\\apache-jmeter-5.6.3\\apache-jmeter-5.6.3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run JMeter') {
            steps {
                bat 'if exist results rmdir /s /q results'
                bat 'mkdir results'
                bat '"%JMETER_HOME%\\bin\\jmeter.bat" -n -t test-plans\\restful-booker_demo.jmx -l results\\results.jtl -e -o results\\report'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'results/**', allowEmptyArchive: true
            publishHTML(target: [
                reportDir: 'results/report',
                reportFiles: 'index.html',
                reportName: 'JMeter Dashboard',
                keepAll: true,
                allowMissing: false,
                alwaysLinkToLastBuild: true
            ])
        }
    }
}
