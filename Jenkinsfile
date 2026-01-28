pipeline {
  agent any

  tools {
    maven 'Maven_3'      // uses the Maven tool you configured in Jenkins
    // jdk 'JDK21'       // add only if you configured a JDK tool in Jenkins Tools
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build and Test') {
      steps {
        bat 'mvn clean test package'
      }
    }
  }

  post {
    always {
      junit 'target/surefire-reports/*.xml'
    }
  }
}
