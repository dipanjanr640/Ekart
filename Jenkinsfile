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
    stage ('mvn build') {
      steps {
        sh "mvn clean install"
      }
    }
    stage ('sonar scanner analysis') {
      steps {
        withSonarQubeEnv('sonar-server') {
          sb '''mvn clean verify sonar:sonar \
  -Dsonar.projectKey=ekart-app \
  -Dsonar.host.url=http://172.211.30.74:9000 \
  -Dsonar.login=sqp_24c3a0762c6f7f72b922cf359e8d2329833510db'''
        }
      }
    }    
  }
}
