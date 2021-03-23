pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Unit Test'
        sh 'mvn test'
        junit '**/target/surefire-reports/*.xml'
        hygieiaCodeQualityPublishStep checkstyleFilePattern: '', findbugsFilePattern: '', jacocoFilePattern: '', junitFilePattern: 'target/surefire-reports/*.xml', pmdFilePattern: ''
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
        hygieiaBuildPublishStep buildStatus: 'Success'
        echo 'Deploy to Stage'
        sh 'mvn clean install'

        echo 'User Acceptance Test'
        sh 'mvn test'
        junit '**/target/surefire-reports/*.xml'
        hygieiaCodeQualityPublishStep checkstyleFilePattern: '', findbugsFilePattern: '', jacocoFilePattern: '', junitFilePattern: 'target/surefire-reports/*.xml', pmdFilePattern: ''
      }
    }

  }
  tools {
    maven 'mvn-3.5.4'
  }
}

