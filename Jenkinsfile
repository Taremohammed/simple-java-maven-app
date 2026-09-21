pipeline {
    agent any

    tools {
        jdk 'Java21'
        maven 'Maven'
    }

    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deliver') {
            steps {
                bat 'mvn -B jar:jar install:install'
                bat 'java -jar target/my-app-1.0-SNAPSHOT.jar'
            }
        }
    }
}
