pipeline {
    environment {
        registry = "20.115.32.204:8085/chatapp"
        registryCredential = 'nexus-hub'
        dockerImage = ''
    }
    agent any 
    // agent is where my pipeline will be eexecuted
    tools {
        //install the maven version configured as m2 and add it to the path
        maven "mvn1"
    }
    stages {
        stage('pull from scm') {
            steps {
            git credentialsId: 'gitlab-credential', url: 'https://github.com/gopal1409/springchat1.git'
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
                  docker.withRegistry('http://20.115.32.204:8085',registryCredential) {
                      dockerImage.push()
                  }
                }
            }
        }
    }
}
