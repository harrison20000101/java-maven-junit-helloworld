pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn test'
        echo 'Unit Testing'
      }
    }

    stage('Test') {
      steps {
        echo 'Integration Testing'
        sh 'mvn verify'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying'
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