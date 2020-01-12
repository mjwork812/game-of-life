pipeline {
  options {
    ansiColor('xterm')
  }

  agent any

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
