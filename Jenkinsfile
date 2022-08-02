
pipeline {
  agent any
  tools {
    maven 'maven2'
  }
  stages{
    stage("Maven Build"){
      steps{
        sh "mvn clean package"
      }
    }
    stage("Deploy To Dev"){
      steps{
        tomcatDeploy("tomcat-dev","ec2-user",["172.31.15.186","172.31.15.186"])
      }
    }
  }
}
