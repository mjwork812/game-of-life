pipeline {
  options {
    ansiColor('xterm')
  }

  agent any

  tools {
    maven 'maven-latest'
  }

  stages {

    stage('Prepare') {
      steps {
        // checkout scm
        git credentialsId: 'mj-key', url: 'https://github.com/mjwork812/game-of-life.git'
      }
    }

    stage('Verify') {
      steps {
        sh 'mvn verify'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always {
          junit '**/target/surefire-reports/*.xml'
        }
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

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
