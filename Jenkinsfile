pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''echo "Executing shell script"
script scripts/build.sh
echo "Finished execution"'''
        script {
          checkout scm

          docker build -t denisimage
        }

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

  }
  environment {
    registry = 'generatorp/jenkinspipe'
  }
}