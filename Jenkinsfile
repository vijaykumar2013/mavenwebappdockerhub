pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Docker_token')
  }

    stages {
        stage('code fetch') {
            steps {
                git branch: 'main', url: 'https://github.com/vjtechie/mavenwebappdockerhub.git'
            }
        }
        stage('Build packages') {
            steps {
                sh "mvn clean package"
            }
        }
         stage('Build') {
      steps {
        sh 'docker build -t vijaysvk333/pipelienerepo .'
      }
    }
         
        stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push vijaysvk333/pipelienerepo'
      }
    }
    }
}
