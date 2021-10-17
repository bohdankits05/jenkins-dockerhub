pipeline {
    agent { label 'master' }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('67596594-5bde-46b0-8485-db87fff87f97')
    }

    stages {

        stage('Checkout') {
            steps{
                git branch: 'main', url: 'git@github.com:bohdankits05/jenkins-dockerhub.git'
            }
        }

        stage('Build') {
            steps{
                sh 'docker build -t devops14:latest .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('ImageTag') {
            steps {
                sh 'docker tag devops14:latest bkits/devops14-docker:version2'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push bkits/devops14-docker:version2'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
