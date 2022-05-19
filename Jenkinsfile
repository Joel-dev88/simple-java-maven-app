pipeline {
  agent {
    label 'agent1'
  }
  tools {
    maven 'maven384'
  }
  
  options {
    timestamps
    timeout(10)
    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')
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
        sh "mvn clean install -DskipTests"
      }
    }
    stage('test') {
      steps {
        sh "mvn test"
        junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
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


