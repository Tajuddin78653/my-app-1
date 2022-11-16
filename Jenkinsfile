
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
                            sshagent (['Otomcat'])
                             {
                               sh "mv target/*.war target/webapp.war"
                               sh "scp -o StrictHostKeyChecking=no target/webapp.war ec2-user@172.31.11.226:/opt/tomcat-stage/webapps/"
                               sh "ssh ec2-user@172.31.11.226 /opt/tomcat-stage/bin/shutdown.sh"
                               sh "ssh ec2-user@172.31.11.226 /opt/tomcat-stage/bin/startup.sh"
                             }
                           }
                         }
  }
}
