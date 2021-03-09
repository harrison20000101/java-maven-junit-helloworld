pipeline {
    agent any
    
    tools {
        maven 'mvn-3.6.3'
    }
    stages {
        stage('Build') {
            steps {
                def os = System.properties['os.name'].toLowerCase()
                echo "OS: ${os}"
                if (os.contains("linux")) {
                    sh "mvn install" 
                } else {
                    bat "mvn install"
                }
            }
        }
    }
    post {
        always {
            junit testresults:"**/target/surefire-reports/*.xml"
        }
    }
}
