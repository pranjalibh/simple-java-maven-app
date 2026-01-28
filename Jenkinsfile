pipeline {
  agent any

  tools {
    maven 'Maven_3'
    // jdk 'JDK21'   // add this only if you configured a JDK tool in Jenkins
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build and Test') {
      steps {
        bat 'mvn -version'
        bat 'mvn clean test package'
      }
    }
  }
}
