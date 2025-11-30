post {
    success {
        emailext(
            to: 'trabelsisabri5@outlook.fr',
            subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Build OK: ${env.BUILD_URL}"
        )
    }
    failure {
        emailext(
            to: 'trabelsisabri5@outlook.fr',
            subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Build FAILED: ${env.BUILD_URL}console"
        )
    }
}
