post {
    success {
        emailext(
            to: 'trabelsisabri5@gmail.com',
            subject: "SUCCESS ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Build OK: ${env.BUILD_URL}"
        )
    }
}
