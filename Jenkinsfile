pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-pwd')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/kudos1430/JENKINS.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t valaxy/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker tag d022d8f4f0dc 14300341/jenkins'
                sh 'docker push 14300341/jenkins'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

