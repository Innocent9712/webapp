pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
    stage('Initialize') {
      steps {
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage ('Deploy-To-Tomcat') {
      steps {
        sshagent(['tomcat']) {
          sh '''
            scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.87.208.75:/tmp/
            ssh -o StrictHostKeyChecking=no ubuntu@3.87.208.75 "sudo mv /tmp/*.war /opt/tomcat/webapps/ && sudo chown tomcat:tomcat /opt/tomcat/webapps/*.war"
          '''
        }      
      }       
    }
  }
}
