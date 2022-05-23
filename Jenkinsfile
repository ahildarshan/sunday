pipeline {
  agent any
  stages {
    stage ('compile') {
      steps {
        bat 'mvn compile'
      }
    }
    stage ('test') {
      steps {
        bat 'mvn test'
      }
    }
    stage ('build') {
      steps {
        bat 'mvn package'
      }
    }
  }
}
