pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''
                    echo "PATH = %PATH%"
                    echo "M2_HOME = %M2_HOME%"
                '''
      }
    }
    stage('Build') {
      steps {
        sh 'cd NumberGenerator && mvn install'
      }
      post {
        success {
          junit 'NumberGenerator/target/surefire-reports/*.xml'
          
        }
        
      }
    }
    stage('Quality Analyse') {
      steps {
        sh 'cd NumberGenerator && mvn clean verify sonar:sonar'
      }
    }
  }
  tools {
    maven 'maven3.1.1'
    jdk 'java8'
  }
}