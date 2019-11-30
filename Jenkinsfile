pipeline {
  agent any

  tools {
    maven 'apache-maven-3.6.0'
  }

  stages {

    stage('Prepare') {
      steps {
        // checkout scm
        git credentialsId: 'mj-key', url: 'ssh://matthew@192.168.1.205/export/groups/gitrepos/game-of-pipelines.git'
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
