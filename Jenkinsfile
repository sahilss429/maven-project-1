pipeline {
  agent any
  
  parameters {
    string(name: 'tomcat_dev', defaultValue: '192.168.10.11', description: 'Staging Server')
    string(name: 'tomcat_prod', defaultValue: '192.168.10.12', description: 'Production Server')
    string(name: 'tomcat_path', defaultValue: '/opt/tomcat/webapps', description: 'Tomcat Path')
  }
  
  triggers {
    pollSCM('* * * * *')
  }
  
  
  stages{
    stage('Build'){
      steps {
        sh '/opt/apache-maven-3.6.3/bin/mvn clean package'
      }
      post {
        success {
          echo 'Now archiving'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    stage ('Deployments'){
      parallel{
        stage ('Deploy to Staging'){
          steps {
            sh "scp **/target/*.war root@${params.tomcat_dev}:${params.tomcat_path}"
          }
        }
        stage ("Deploy to Production"){
          steps {
            sh "scp **/target/*.war root@${params.tomcat_prod}:${params.tomcat_path}"
          }
        }
      }
    }
  }
}
