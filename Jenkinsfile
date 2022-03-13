pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         
    } 

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
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
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war root-user@${params.tomcat_dev}:/var/lib/Apache Tomcat/9.0.59/webapps"
                    }
                }

            }
        }
    }
}
