pipeline {
    agent any

    stages {

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('src') {
                        sh 'docker build -t abhiramnaresh/cartservice:latest .'
                    }
                }
            }
        }

        stage('Scan') {
            steps {
                sh 'trivy image abhiramnaresh/cartservice:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'docker push abhiramnaresh/cartservice:latest'
                    }
                }
            }
        }

    }
}
