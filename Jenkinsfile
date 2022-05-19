pipeline {
  agent {
    label 'agent1'
  }
  tools {
    maven 'maven384'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh "echo $PATH"
        sh "mvn clean install"
      }
    }
    stage('test') {
      steps {
        sh "mvn test"
      }
    }
    stage('Post tasks') {
      steps {
        sh "echo send an email"
      }
    }
  }
}
//Declarative


