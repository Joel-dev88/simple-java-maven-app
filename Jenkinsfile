pipeline {
  agent {
    label 'agent1'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh "mvn clean install"
      }
    }
    stage('test') {
      steps {
        sh "mvn test"
      }
    }
  }
}
