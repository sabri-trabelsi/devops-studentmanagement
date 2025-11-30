node {

    stage('Checkout') {
        echo '📥 Checkout source code'
        checkout scm
    }

    stage('Build') {
        echo '🚀 Build DevOps Student Management (Maven)'
        sh 'mvn -version'
        sh 'mvn clean package -DskipTests'
    }

    stage('Test') {
        echo '🧪 Running Maven tests'
        sh 'mvn test'
    }

    stage('Notify') {
        // Slack notif
        slackSend(
            channel: '#jenkins',
            color: (currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger'),
            message: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${env.BUILD_URL}"
        )

        // Email notif
        emailext(
            to: 'trabelsisabri5@gmail.com',   // ou ton Outlook si tu préfères
            subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """Result: ${currentBuild.currentResult}
Job: ${env.JOB_NAME}
Build: #${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
"""
        )
    }
}
