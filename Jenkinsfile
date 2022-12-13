pipeline {
    
    agent {
        docker {
            image 'node:16-alpine'
        }
    } 

    stages {

        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
        
        // stage("Building Docker Image") {

        //     steps {
        //         sh "docker build -t inventory-lord:1.0 ."
        //     }

        // }

		// stage("Trivy scanning") {

        //     steps {
        //         sh "docker run aquasec/trivy image inventory-lord:1.0 -f json -o results.json"
        //         recordIssues(tools: [trivy(pattern: 'results.json')])
        //     }

        // }

    }
}
