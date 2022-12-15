pipeline {
    
    agent {
        label 'trivy'
    } 

    environment {
        TEMPLATE_PATH="\"@/root/templates/html.tpl\""
    }

    stages {
        
        stage("Building Docker Image") {

            steps {
                sh "docker build -t inventory-lord:1.0 ."
            }

        }

		stage("Trivy scanning") {

            steps {
                sh "trivy image --format template -t ${TEMPLATE_PATH} --output report.html inventory-lord:1.0"
            }

        }

    }

    post {
        always {
            archiveArtifacts artifacts: "report.html", fingerprint: true

            publishHTML (target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: '.',
                reportFiles: 'report.html',
                reportName: "Trivy Image Vuln Report"
            ])
        }
    }
}
