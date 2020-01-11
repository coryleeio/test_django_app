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
  - name: docker
    image: docker:19.03.1
    command:
    - sleep
    args:
    - 99d
    env:
      - name: DOCKER_HOST
        value: tcp://localhost:2375
  - name: docker-daemon
    image: docker:19.03.1-dind
    securityContext:
      privileged: true
    env:
      - name: DOCKER_TLS_CERTDIR
        value: ""
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
        container('docker') {
            sh 'docker version && docker build .'
        }
      }
    }

    stage('Test') {
        parallel {
            stage('Test shard1') {
              steps {
                container('docker') {
                    sh 'docker images'
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

    stage('Promote') {
        parallel {
            stage('Promote to Prod') {
              steps {
                container('maven') {
                  sh 'mvn -version'
                }
                container('busybox') {
                  sh '/bin/busybox'
                }
              }
            }
            stage('Promote to Edge') {
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
