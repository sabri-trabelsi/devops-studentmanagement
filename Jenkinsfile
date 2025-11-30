post {
    success {
        emailext(
            to: 'trabelsisabri5@gmail.com',
            subject: "TEST JENKINS SABRI SUCCESS #${env.BUILD_NUMBER}",
            body: "Build OK: ${env.BUILD_URL}"
        )
    }
    failure {
        emailext(
            to: 'trabelsisabri5@gmail.com',
            subject: "TEST JENKINS SABRI FAILED #${env.BUILD_NUMBER}",
            body: "Build FAILED: ${env.BUILD_URL}console"
        )
    }
}
