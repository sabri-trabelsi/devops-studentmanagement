pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🚀 Build DevOps Student Management'
                sh 'date'
            }
        }
    }

    post {
        success {
            emailext(
                to: 'trabelsisabri5@gmail.com',
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build OK: ${env.BUILD_URL}"
            )
        }
        failure {
            emailext(
                to: 'trabelsisabri5@gmail.com',
                subject: "❌ FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build FAILED: ${env.BUILD_URL}console"
            )
        }
    }
}
