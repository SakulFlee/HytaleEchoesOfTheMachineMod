pipeline {
  agent {
    kubernetes {
      label 'k8s'
      defaultContainer 'java'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: java
    image: eclipse-temurin:25-jdk-ubi10-minimal 
    imagePullPolicy: Always
    command: ["cat"]
    tty: true
"""
    }
  }

  stages {
    stage('Build & Package') {
      steps {
        container('java') {
          sh 'mvn package'
        }
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/**/*.jar', fingerprint: true
    }
  }
}

