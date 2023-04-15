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
    stage ('Check-Git-Secrets') {
      steps {
        sh 'docker run --rm gesellix/trufflehog --json https://github.com/Innocent9712/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/Innocent9712/webapp/master/owasp-dependency-check-new.sh" '
         sh 'chmod +x owasp-dependency-check-new.sh'
         sh 'bash owasp-dependency-check-new.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/odc-reports/dependency-check-report.xml'
        
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
            ssh -o StrictHostKeyChecking=no ubuntu@3.87.208.75 "sudo mv /tmp/*.war /opt/tomcat/webapps/ && sudo find /opt/tomcat/webapps/ -maxdepth 1 -name "*.war" -exec chown tomcat:tomcat {} +"
          '''
        }      
      }       
    }
  }
}
