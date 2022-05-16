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
        sh "mvn --version"
        sh "mvn clean install"
      }
    }
  }
}
