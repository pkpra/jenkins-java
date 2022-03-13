pipeline {
    agent any
    environment {
       PATH = "/opt/maven3/bin:$PATH"
       }
    stages {
        stage('Git checkout') {
            steps { 
                git credentialsId: '121', url: 'https://github.com/pkpra/jenkins-java.git'
            }
        }
       
        stage('Deploy') {
            steps {
                  sshagent(credentials: ['iam'], ignoreMissing: true) {
                  sh """
                         scp target/myweb.war root@ip-172-31-85-44:/home/ubuntu/apache-tomcat-9.0.59/webapps
                         sh root@ip-172-31-85-44:/home/ubuntu/apache-tomcat-9.0.59/bin/shutdown.sh
                         sh root@ip-172-31-85-44:/home/ubuntu/apache-tomcat-9.0.59/bin/startup.sh
                  """
              }
            } 
        }
    }
}
