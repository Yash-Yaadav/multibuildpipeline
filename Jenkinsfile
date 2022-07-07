pipeline {
    agent any
    tools {
        maven "m3"
    }
    stages {
        stage('checkout scm') {
            steps {
                git branch: 'main', url: 'https://github.com/Yash-Yaadav/chatapp-jenkis.git'
            }
        }   
        stage('mvn build'){
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('mvn test'){
            steps {
                sh "mvn test"
            }
        }
        stage('test report'){
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('check style'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('check style view'){
            steps {
                recordIssues(tools: [checkStyle(pattern: 'target/checkstyle-result.xml')])
            }
        }
        stage('ansible prov'){
            steps {
               ansiblePlaybook credentialsId: 'root', inventory: 'dev.inv', playbook: 'tomcat.yml'
            }
        }
         
    }
}
