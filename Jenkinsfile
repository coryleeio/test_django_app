pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
  - name: busybox
    image: busybox
    command:
    - cat
    tty: true
"""
    }
  }
  stages {
    stage('Build') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }

    stage('Test') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }

    stage('Publish') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }

    stage('Deploy Stage') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }


    parallel{
      stage('Deploy Prod') {

        steps {
          container('maven') {
            sh 'mvn -version'
          }
          container('busybox') {
            sh '/bin/busybox'
          }
        }
      }

      stage('Deploy Edge') {
        steps {
          container('maven') {
            sh 'mvn -version'
          }
          container('busybox') {
            sh '/bin/busybox'
          }
        }
      }
    }




  }
}
