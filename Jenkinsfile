pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        script {
          checkout scm
        }

      }
    }

    stage('Application Build') {
      steps {
        script {
          sh scripts/build.sh
        }

      }
    }

  }
  environment {
    registry = 'piokwa/cicdtask'
  }
}