pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing'
          }
        }

        stage('onother testing') {
          steps {
            echo 'other testing'
          }
        }

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