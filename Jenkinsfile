pipeline {
  agent { label 'slave' }
    tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
    }
  stages {
   stage ('Maven Build') {
      steps {
        sh "mvn clean install"
      }
    }
  }
}
