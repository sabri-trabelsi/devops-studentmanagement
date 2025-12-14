pipeline {
    agent any

    environment {
        SONAR_LOGIN  = credentials('sonarqube-token')
        DOCKER_IMAGE = "sabritr/student-management:1.0.0"
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
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
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

        stage('Docker Build & Push') {
            steps {
                sh """
                  docker build -t ${DOCKER_IMAGE} .
                  docker push ${DOCKER_IMAGE}
                """
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                sh """
                  kubectl apply -f k8s/ -n devops
                  kubectl rollout status deployment/spring-app -n devops
                """
            }
        }
    }

    post {
        success {
            slackSend(
                channel: 'jenkins',
                color: '#36a64f',
                message: "SUCCESS: `${env.JOB_NAME}` #${env.BUILD_NUMBER}\n${env.BUILD_URL}"
            )
        }
        failure {
            slackSend(
                channel: 'jenkins',
                color: '#FF0000',
                message: "FAILURE: `${env.JOB_NAME}` #${env.BUILD_NUMBER}\n${env.BUILD_URL}"
            )
        }
    }
}
