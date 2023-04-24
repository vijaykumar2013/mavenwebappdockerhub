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
         stage('Build Imange') {
           steps {
             sh 'docker build -t vijaysvk333/pipelienerepo:v1.$BUILD_ID .'
           }
        }
         
        stage('Login to DockeHub') {
          steps {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          }
        }
        stage('Push to DockerHub') {
          steps {
            sh 'docker push vijaysvk333/pipelienerepo:v1.$BUILD_ID'
          }
        }
        stage('Deploy App on k8s') {
          steps {
            sshagent(['k8s']) {
              sh "scp -o StrictHostKeyChecking=no mavenwebapp.yaml ubuntu@182.18.184.69:/home/ubuntu"
              script {
                try{
                  sh "ssh ubuntu@182.18.184.69 kubectl create -f ."
                }catch(error){
                    sh "ssh ubuntu@182.18.184.69 kubectl create -f ."
            }
}
        }
      
    }
    }
    }
}
