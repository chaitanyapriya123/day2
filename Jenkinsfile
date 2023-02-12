pipeline {
//      environment {
//     imagename = "chaitanyapriya/image2"
// //     dockerImage = ''
//      }
    agent any
    options { 
        timestamps ()
        timeout(time: 2, unit: 'SECONDS')   
        skipDefaultCheckout true
        buildDiscarder(logRotator(daysToKeepStr: '10'))
    }
    stages {
        stage('Display Docker version') {
            steps {
                sh 'docker --version'
            }
        }
        stage('Display Git version') {
            steps {
                sh 'git --version'
            }
        }
        stage('Code checkout') {
             steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chaitanyapriya123/day2.git']])  
             }
        }
         stage('Building image') {
              steps{
                   script {
                       retry(2){
                        sh docker image prune -a
                        docker build -t imageapache:${BUILD_NUMBER} .
                        docker images
                        docker image inspect httpd:2.4
                        docker run -d -t --name apachecontainer httpd:2.4
                        docker ps -aq | xargs docker stop 
                       }
                   }
              }
         }
    }
}
