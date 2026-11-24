
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image1 .'
            }
        }

        stage('Tag') {
            steps {
                sh 'docker tag image1 myrepo/paytm:bank'
            }
        }

        stage('Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        sh 'docker push myrepo/paytm:bank'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f bank-app || true
                    docker run -d --name bank-app -p 1111:80 myrepo/paytm:bank
                '''
            }
        }
    }
}

