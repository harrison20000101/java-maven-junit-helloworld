pipeline {
    agent any
    
    tools {
        maven 'mvn-3.6.3'
    }
    stages {
        stage('Build') {
            steps {
                sh "mvn test" 
            }
        }
    }
    post {
        always {
            junit testresults:"**/target/surefire-reports/*.xml"
        }
    }
}
