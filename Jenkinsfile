pipeline {
    agent any

stages{
    stage('Git Checkout'){
                   steps{
                   git credentialsId: '11', url: 'https://github.com/pkpra/jenkins-java.git'
              }
          }
    stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
           
                    steps {
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war root-user@ip-172-31-85-44::/var/lib/Apache Tomcat/9.0.59/webapps"
                    }
        }
    }
}
