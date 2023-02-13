pipeline {
     environment {
     imagename = "chaitanyapriya/task"
     dockerImage = ''
}
    agent any
    options { 
        timestamps ()
        timeout(time: 2, unit: 'MINUTES')   
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
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/chaitanyapriya123/day2.git']])
             }
        }
         stage('Building image') {
              steps{
                   script {
                       sh docker images
                        docker image prune -a
                        docker build -t tasks .
                        docker images
                        docker image inspect httpd:2.4
                        docker ps -aq | xargs docker stop
             
                       
                   }
              }
         }
    }
}

