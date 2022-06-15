pipeline{
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '4c93ad9e-4817-4f0e-bee5-ff24ea921c53', url: 'https://github.com/devopshint/jenkins-docker-example.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t pavan7416/my-app-1.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'pavan7416', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u pavan7416 -p ${dockerhubpwd}'
                 }  
                 sh 'docker push pavan7416/my-app-1.0'
                }
            }
        }
    }
}
