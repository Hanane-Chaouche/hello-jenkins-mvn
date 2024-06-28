pipeline {
    agent any
    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk1.8.0_202'
        MAVEN_HOME = 'C:\\Users\\rehou\\Documents\\apache-maven-3.9.0\\bin'
        PATH = "${env.PATH};${env.JAVA_HOME}\\bin;${env.MAVEN_HOME}"
    }
    stages {
        stage('Checkout') {
            steps {
                // Cloner le repository depuis GitHub
                git branch: 'main', url: 'https://github.com/hrhouma/hello-jenkins-mvn.git'
            }
        }

        stage('Build') {
            steps {
                // Nettoyer et compiler le projet avec Maven
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests unitaires
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Packager le projet en JAR
                bat 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archiver les artefacts générés (JAR)
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Publier les résultats des tests, si disponibles
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
