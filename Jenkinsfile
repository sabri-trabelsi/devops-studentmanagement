node {
    stage('Build') {
        echo '🚀 Build DevOps Student Management'
        sh 'date'
    }

    stage('Notify') {
        emailext(
            to: 'trabelsisabri5@gmail.com', 
            subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """Result: ${currentBuild.currentResult}
Job: ${env.JOB_NAME}
Build: #${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
"""
        )
    }
}
