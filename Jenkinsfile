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
    

stage('Build and Test') {
      steps {
        bat 'mvn clean test package'
      }
    }
    

stage('UI Tests (Selenium)') {
  
    steps {

    parameters {
    booleanParam(
        name: 'RUN_UI_TESTS',
        defaultValue: false,
        description: 'Run Selenium UI tests'
    )
 }
    when {
        expression { return params.RUN_UI_TESTS }
    }
        bat 'mvn -B verify -DskipUnitTests=true'
    }
}

}

  post {
    always {
      //junit 'target/surefire-reports/*.xml'
      junit allowEmptyResults: true, testResults: '''
            target/surefire-reports/*.xml,
            target/failsafe-reports/*.xml
        '''

    }
  }
}
