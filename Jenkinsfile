pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Test') {
      steps {
        sh 'testing'
      }
    }

  }
  tools {
    maven 'mvn-3.6.3'
  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
    }

  }
}