pipeline {
  agent any
  stages{
    stage('Init'){
      steps {
        echo "Testing..."
      }
    }

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
    }

    stage('Validate'){
      steps {
        echo "Validating..."
      }
    }

    stage('Deploy to Staging'){
      steps {
        build job: 'Deploy-to-staging'
      }
    }
  }
}
