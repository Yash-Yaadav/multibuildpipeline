pipeline {
        environment {
        registry = "52.255.179.237:8085/yash059/chatappnormal"
        registryCredential = 'nexus cre'
        dockerImage = ''
    }
    agent any 
    // agent is where my pipeline will be eexecuted
    tools {
        //install the maven version configured as m2 and add it to the path
        maven "m3"
    }
    stages {
        stage('pull from scm') {
            steps {
            git credentialsId: 'gittoken', url: 'https://github.com/gopal1409/springchat1.git'
            }
        }
                 stage('build it') {
            steps {
            sh 'mvn clean package'
            }
        }
        stage('docker image') {
            steps {
                script {
                  dockerImage=docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('docker push') {
            steps {
                script {
                  docker.withRegistry('http://52.255.179.237:8085',registryCredential) {
                      dockerImage.push()
                  }
                }
            }
        }
    }
}
