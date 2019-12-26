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
        sh 'mvn clean package'
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

    stage('Deploy'){
      steps {
        echo "Deploying..."
      }
    }
  }
}
