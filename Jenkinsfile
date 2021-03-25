pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'PMD Check'
        sh 'mvn pmd:pmd'
        
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
        hygieiaDeployPublishStep applicationName: 'CI Demo App', artifactDirectory: '**/target', artifactGroup: 'com.example.javamavenjunithelloworld', artifactName: '*.jar', artifactVersion: '', buildStatus: 'Success', environmentName: 'Dev'
        }
    }

  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      pmd(canRunOnFailed: true, pattern: '**/target/pmd.xml')
    }
  }
  tools {
    maven 'mvn-3.5.4'
  }
}

