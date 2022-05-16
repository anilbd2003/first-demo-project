pipeline {
  agent any
  tools {
  Maven 'maven'  
  }

  stages{
    stage('Initialize'){
      steps {
      sh '''
          echo "PATH=${PATH}"
          echo "M2_HOME= ${M2_HOME}"
          '''
      }
    }  
    stage('Build') {
      steps {
        sh 'mvn clean package'
        }
     }
    stage('deploy to tomcat') {
      steps {
        sshagent(['tomcat']) {
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.84.211.81:/home/ubuntu/prod/apache-tomcat-8.5.78/webapps/webapp.war'
        }
      
      }
    }
  }
}
