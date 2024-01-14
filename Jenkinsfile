pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        agent {
                docker {
                    image 'node:20.10.0-alpine3.19'
                    // Run the container on the node specified at the
                    // top-level of the Pipeline, in the same workspace,
                    // rather than on a new node entirely:
                    reuseNode true
                }
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

  }
}
