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
          def customImage = docker.build("${registry}:${env.Build_ID}")
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

    stage('Deliver') {
      environment {
        registry = 'generatorp/jenkinspipe'
      }
      steps {
        script {
          docker.withRegistry("${registry}")
          {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
          }
        }

      }
    }

  }
  environment {
    registry = 'generatorp/jenkinspipe'
  }
}