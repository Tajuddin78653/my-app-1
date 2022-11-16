
pipeline {
  agent any
  tools {
    maven 'maven01'
  }
  stages{
    stage("Maven Build"){
      steps{
        sh "mvn clean package"
      }
    }
                         stage("Deploy To Dev"){
                           steps{
                            sshagent (['tomcat-dev'])
                             {
                               sh "mv target/*.war target/webapp.war"
                               sh "scp -o StrictHostKeyChecking=no target/webapp.war ec2-user@172.31.11.226:/opt/tomcat9/webapps/"
                               sh "ssh ec2-user@172.31.11.226 /opt/tomcat9/bin/shutdown.sh"
                               sh "ssh ec2-user@172.31.11.226 /opt/tomcat9/bin/startup.sh"
                             }
                           }
                         }
  }
}
