pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''chmod +x scripts/build.sh
./scripts/build.sh'''
      }
    }

    stage('test') {
      steps {
        sh '''chmod +x scripts/test.sh
./scripts/test.sh
'''
      }
    }

    stage('docker image build') {
      steps {
        sh 'docker build -t aibabll/mybuildimage'
      }
    }

  }
}