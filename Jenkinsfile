pipeline {
    agent {
        node {
            label 'slave_build'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Checkout source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '🚀 Build Maven on agent slave_01'
                bat 'mvn -version'
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Tests Maven'
                bat 'mvn test'
            }
        }
    }

    post {
        always {
            slackSend(
                channel: '#jenkins',
                color: (currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger'),
                message: """Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}
Agent: slave_01
URL: ${env.BUILD_URL}
Commit: ${env.GIT_COMMIT}"""
            )
        }
    }
}
