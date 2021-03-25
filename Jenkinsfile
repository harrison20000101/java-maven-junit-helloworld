pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Unit Test'
        sh 'mvn test sonar:sonar -Dsonar.projectKey=test -Dsonar.host.url=http://69.230.231.193:9000 -Dsonar.login=6117ef30bce15f0daf675712fa04e49f64b672df'
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
        hygieiaDeployPublishStep applicationName: 'CI Demo App', artifactDirectory: '**/target/', artifactGroup: 'com.example.javamavenjunithelloworld', artifactName: '*.jar', artifactVersion: '', buildStatus: 'Success', environmentName: 'Dev'
        }
    }

  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      hygieiaCodeQualityPublishStep checkstyleFilePattern: '**/*/checkstyle-result.xml', findbugsFilePattern: '**/*/Findbugs.xml', jacocoFilePattern: '**/*/jacoco.xml', junitFilePattern: '**/*/TEST-.*-test.xml', pmdFilePattern: '**/*/PMD.xml'
    }
  }
  tools {
    maven 'mvn-3.5.4'
  }
}

