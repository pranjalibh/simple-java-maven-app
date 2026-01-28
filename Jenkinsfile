pipeline {
  agent any

  tools {
    maven 'Maven_3'
    // jdk 'JDK21'   // enable only if you configured this in Jenkins Tools
  }

  parameters {
    booleanParam(
      name: 'RUN_UI_TESTS',
      defaultValue: false,
      description: 'Run Selenium UI tests'
    )
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build and Unit Tests') {
      steps {
        bat 'mvn clean test package'
      }
    }

    stage('UI Tests (Selenium)') {
      when {
        expression { return params.RUN_UI_TESTS }
      }
      steps {
        // Run integration/UI tests (commonly via failsafe)
        bat 'mvn -B verify -DskipUnitTests=true'
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: '''
        target/surefire-reports/*.xml,
        target/failsafe-reports/*.xml
      '''
    }
  }
}
