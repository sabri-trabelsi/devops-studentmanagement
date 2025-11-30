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
                sh 'mvn -version'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Tests Maven'
                sh 'mvn test'
            }
        }

        stage('Notify') {
            steps {
                slackSend(
                    channel: '#jenkins',
                    color: (currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger'),
                    message: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER} (agent: slave_01)"
                )
            }
        }
    }
}
