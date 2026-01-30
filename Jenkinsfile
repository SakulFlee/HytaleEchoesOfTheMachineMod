pipeline {
  agent {
    kubernetes {
      label 'k8s'
      defaultContainer 'rust'
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
    stage('Build') {
      steps {
        container('java') {
          sh './gradlew build'
        }
      }
    }
    
    stage('Package') {
      steps {
        container('java') {
          sh './gradlew shadowJar'
        }
      }
    }
  }
}

