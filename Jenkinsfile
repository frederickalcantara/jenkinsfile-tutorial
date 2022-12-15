pipeline {
    
    agent {
        label 'trivy'
    } 

    stages {

        // stage('Test') {
        //     steps {
        //         sh 'node --version'
        //     }
        // }
        
        stage("Building Docker Image") {

            steps {
                sh "docker build -t inventory-lord:1.0 ."
            }

        }

		stage("Trivy scanning") {

            steps {
                sh "trivy image --format template -t \"/root/templates/html.tpl\" --output report.html inventory-lord:1.0"
            }

        }

    }

    post {
        always {
            archiveArtifacts artifacts: "report.html", fingerprint: true

            publishHTML (target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: truem
                reportDir: '.',
                reportFiles: 'report.html',
                reportName: "Trivy Image Vuln Report"
            ])
        }
    }
}
