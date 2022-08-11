pipeline {
  agent { 
    label 'slave' 
  }
  tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
  }
  stages {
    stage('Initialize'){
      steps{
          echo "PATH = ${M2_HOME}/bin:${PATH}"
          echo "M2_HOME = /opt/maven"
      }
    }
    stage ('Build') {
      environment {
	       scannerHome = tool 'SonarQube Scanner'
	    }
      steps {
         withSonarQubeEnv('admin') {
            sh "mvn clean verify install sonar:sonar -Dsonar.projectKey=mavenproject"
         }
      }
    }
  }
}
