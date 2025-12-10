pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build Maven'
                sh 'mvn -version'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests Maven'
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            slackSend(
                channel: '#jenkins',
                color: (currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger'),
                message: """Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}
Agent: ${env.NODE_NAME}
URL: ${env.BUILD_URL}
Commit: ${env.GIT_COMMIT}"""
            )
        }
    }
}
