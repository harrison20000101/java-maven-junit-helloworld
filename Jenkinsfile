pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Unit Test'
        sh 'mvn test'
      }
    }

    stage('Test') {
      steps {
        echo 'Build Success, push to QA'
        hygieiaBuildPublishStep buildStatus: 'Success'

        echo 'Integration Testing'
        sh 'mvn verify'
        step([ $class: 'JacocoPublisher' ])
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy to Stage'

        echo 'User Acceptance Test'
        sh 'mvn clean install'
        }
    }

  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      hygieiaCodeQualityPublishStep checkstyleFilePattern: '', findbugsFilePattern: '', jacocoFilePattern: 'target/site /jacoco-both/*.xml', junitFilePattern: 'target/surefire-reports/*.xml', pmdFilePattern: ''
      archiveArtifact artifacts: 'target/**/*.jar', fingerprint: true
    }
  }
  tools {
    maven 'mvn-3.5.4'
  }
}

