pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Unit Testing'
        sh 'mvn test'
      }
    }

    stage('Test') {
      steps {
        echo 'Integration Testing'
        sh 'mvn verify'
        step([ $class: 'JacocoPublisher' ])
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying'
        echo 'UAT'
        sh 'mvn clean install'
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