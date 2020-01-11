pipeline {
  agent {
    docker {
      image 'ubuntu:latest'
      args 'whoami'
    }

  }
  stages {
    stage('Build') {
      agent {
        docker {
          image 'ubuntu:latest'
          args 'whoami'
        }

      }
      steps {
        sleep 4
      }
    }

  }
}