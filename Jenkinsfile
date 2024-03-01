pipeline {
  agent any
  tools {
    jdk 'jdk17'
    maven 'maven'
    //docker 'docker'
  }
  environment {
    SCANNER_HOME = tool 'sonar-scanner'
    APP_NAME = "ekart-app"
    IMAGE_NAME = "newacr1412421.azurecr.io"+"${APP_NAME}"
  }
  stages{
    stage ('compile') {
      steps {
        sh "mvn compile"
      }
    }
    stage ('test') {
      steps {
        sh "mvn test -DskipTests=true"
      }
    }
    stage ('sonar scanner analysis') {
      steps {
        withSonarQubeEnv('sonar-server') {
          sb '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=ekart-app -Dsonar.projectKey=ekart-app'''
        }
      }
    }    
  }
}
