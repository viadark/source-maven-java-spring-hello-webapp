pipeline {
  agent any

  triggers {
    //pollSCM('* * * * *')
    githubPush()
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/viadark/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://15.164.239.119:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}