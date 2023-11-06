Node {
    def dockerImage = 'node:16-buster-slim'
    
    try {
        checkout scm

        stage('Build') {
            try {
                docker.image(dockerImage).inside("-p 3000:3000", "-v ${pwd()}:/app") {
                    sh 'npm install'
                }
            } finally {
                // Cleanup, if needed
            }
        }
        
        stage('Test') {
            try {
                sh './jenkins/scripts/test.sh'
            } finally {
                // Cleanup, if needed
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
