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

  }
}