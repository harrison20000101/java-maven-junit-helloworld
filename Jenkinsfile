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
        hygieiaBuildPublishStep buildStatus: 'Success'
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
    maven 'mvn-3.5.4'
  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      archiveArtifacts artifacts: 'target/**/*.jar', fingerprint: true
    }

  }
}
