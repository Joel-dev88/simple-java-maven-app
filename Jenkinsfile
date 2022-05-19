pipeline {
  agent {
    label 'agent1'
  }
  tools {
    maven 'maven384'
  }
  
  options {
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
  }
  post {
    always {
      deleteDir()
    }
    failure {
      echo "sendmail -s Maven Job Failed recipients@myco.com"
    }
    success {
      echo "The job is successful"
    }
  }
}

//Declarative


