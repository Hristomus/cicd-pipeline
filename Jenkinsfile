pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''echo "Executing shell script"
script scripts/build.sh
echo "Finished execution"'''
      }
    }

    stage('Test') {
      steps {
        sh '''echo "Start testing"
script scripts/test.sh
echo "Testing finished"
'''
      }
    }

    stage('Build Image') {
      steps {
        script {
          checkout scm
          def app
          app = docker.build("${registry}:${env.Build_ID}")
        }

      }
    }

    stage('Push Image') {
      agent any
      environment {
        registry = 'generatorp/jenkinspipe'
        registryCredential = 'dockerhub_id'
      }
      steps {
        script {
          docker.withRegistry('', registryCredential)
          dockerImage.push()
        }

      }
    }

  }
  environment {
    registry = 'generatorp/jenkinspipe'
    regisrtyCredentials = 'dockerhub_id'
  }
}