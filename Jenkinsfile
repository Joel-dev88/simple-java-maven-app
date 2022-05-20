pipeline {
  agent {
    label 'agent1'
  }
  tools {
    maven 'maven384'
  }
  environment {
    target_user = "ec2-user"
    target_server = "172.31.35.196"
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
    stage('Deploy to Dev') {
      parallel {
        stage('target1'){
          environment {
            target_user = "ec2-user"
            target_server = "172.31.35.196"
          }
          steps {
            echo "Deploying to Dev Enviroment"
            sshagent(['maven-cd-key']) {
              sh "scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar $target_user@$target_server:/home/ec2-user" 
            } 
          }
        }
        stage('target2'){
          environment {
            target_user = "ec2-user"
            target_server = "172.31.36.213"
          }
          steps {
            echo "Deploying to Dev Enviroment"
            sshagent(['maven-cd-key']) {
              sh "scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar $target_user@$target_server:/home/ec2-user" 
            } 
          }
        }
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
//test


/*
    stage('Deploy') {
      steps {
        echo "Deploying to Dev Enviroment"
        sshagent(['maven-cd-key']) {
          sh "scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar $target_user@$target_server:/home/ec2-user" 
        }
      }
    }
*/