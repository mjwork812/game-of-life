pipeline {
  options {
    ansiColor('xterm')
  }

  agent {
    kubernetes {
      label "jenkins-${SERVICE_NAME}-${env.BUILD_ID}"
        defaultContainer 'jenkins-slave-mvn'
        yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: 'jnlp'
    securityContext:
      runAsUser: 1000
    image: maven:latest
    tty: true
    command:
    - cat
  - name: jenkins-slave-mvn
    securityContext:
      runAsUser: 1000
    image: maven:latest
    tty: true
    env:
    command:
    - cat
  restartPolicy: Never
"""
    }
  }

  tools {
    maven 'maven-latest'
  }

  stages {

    stage('SCM Checkout') {
      steps {
        git credentialsId: 'mj-key', url: 'https://github.com/mjwork812/game-of-life.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
      post {
        always {
          junit '**/target/surefire-reports/*.xml'
        }
      }
    }

    // NOT WORKING
    /*
    stage('Dependency Analyzer') {
      steps {
        sh 'mvn dependency:analyze-only'
      }
    }
    */

    /*
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('SonarQube Community Edition') {
          sh 'mvn sonar:sonar'
        }
      }
    }

    stage("Quality Gate") {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
          // true = set pipeline to UNSTABLE, false = don't
          waitForQualityGate abortPipeline: true
        }
      }
    }
    */

    stage('Echo Stuff') {
      steps {
        sh 'echo "Hello World"'
        sh '''
          echo "Multiline shell steps works too"
          ls -laFh
        '''
      }
    }
  }
}
