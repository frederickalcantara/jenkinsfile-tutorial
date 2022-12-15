pipeline {
    
    agent {
       docker { image 'aquasec/trivy:0.35.0' }
    } 

    stages {
        
        stage("Building Docker Image") {

            steps {
                sh "docker build -t inventory-lord:1.0 ."
            }

        }

		stage("Trivy scanning") {

            steps {
                sh "trivy image inventory-lord:1.0 -f json -o results.json"
                recordIssues(tools: [trivy(pattern: 'results.json')])
            }

        }

    }
}