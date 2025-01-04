pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh './scripts/test.sh'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          def app = docker.build("<your-dockerhub-username>/mybuildimage:${env.BUILD_NUMBER}")
          app.push()
          app.push("latest")
        }

      }
    }

  }
  post {
    always {
      cleanWs()
    }

  }
}