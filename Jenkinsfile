pipeline {
    agent any

    environment {
        SONAR_LOGIN = credentials('sonarqube-token')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        mvn sonar:sonar \
                          -Dsonar.projectKey=devops-studentmanagement \
                          -Dsonar.host.url=http://127.0.0.1:9000 \
                          -Dsonar.login=$SONAR_LOGIN
                    '''
                }
            }
        }
    }
}
