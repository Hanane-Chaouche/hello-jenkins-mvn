pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/Hanane-Chaouche/hello-jenkins-mvn.git')
      }
    }

    stage('Build') {
      steps {
        bat 'mvn clean compile'
      }
    }

    stage('Test') {
      steps {
        bat 'mvn test'
      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts(artifacts: 'target/*.jar', allowEmptyArchive: true)
      }
    }

  }
  environment {
        JAVA_HOME = 'C:/Program Files/Java/jdk-17'

        MAVEN_HOME = 'C:/Users/rehou/Documents/apache-maven-3.9.0/bin'
        PATH = "${env.PATH};${env.JAVA_HOME}\\bin;${env.MAVEN_HOME}"
  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
    }

  }
}
