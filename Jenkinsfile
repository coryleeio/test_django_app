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
        parallel {
            stage('Test shard1') {
              steps {
                container('busybox') {
                  sh 'echo shard1'
                }
              }
            }
            stage('Test shard2') {
              steps {
                container('busybox') {
                  sh 'echo shard2'
                }
              }
            }
            stage('Test shard3') {
              steps {
                container('busybox') {
                  sh 'echo shard3'
                }
              }
            }
            stage('Test shard4') {
              steps {
                container('busybox') {
                  sh 'echo shard4'
                }
              }
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

    stage('Deploy to stage') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }

    stage('Release') {
        parallel {
            stage('Deploy to Prod') {
              steps {
                container('maven') {
                  sh 'mvn -version'
                }
                container('busybox') {
                  sh '/bin/busybox'
                }
              }
            }
            stage('Deploy to Edge') {
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
}
