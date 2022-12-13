pipeline {
    agent {
        docker {
            image 'aquasec/trivy:0.35.0'
        }
    } 

    stages {
        
        // stage("Building Docker Image") {

        //     steps {
        //         sh "docker build -t inventory-lord:1.0 ."
        //         recordIssues(tools: [trivy(pattern: 'results.json')])
        //     }

        // }

		stage("Trivy scanning") {

            steps {
                sh "docker run aquasec/trivy image aquasec/trivy:0.35.0 -f json -o results.json"
                recordIssues(tools: [trivy(pattern: 'results.json')])
            }

        }

    }
}
