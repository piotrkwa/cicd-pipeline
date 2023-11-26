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
          sh './scripts/build.sh'
        }

      }
    }

    stage('Tests') {
      steps {
        script {
          sh 'scripts/test.sh'
        }

      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Docker Image Push') {
      steps {
        script {
          docker.withRegistry('','dockerhub_id'){
            docker.image("${registry}:${env.BUILD_ID}").push('latest')
            docker.image("${registry}:${env.BUILD_ID}").push("${env.BUILD_ID}")          }
          }

        }
      }

    }
    environment {
      registry = 'piokwa/cicdtask'
    }
  }