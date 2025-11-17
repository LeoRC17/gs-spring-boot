pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'git@github.com:LeoRC17/gs-spring-boot.git',
                    credentialsId: '0249666d-2801-4e5f-833d-9dafbebba9d1'
            }
        }

        stage('Build') {
            steps {
                echo 'Building fat JAR...'
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn -B test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
