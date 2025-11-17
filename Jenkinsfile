pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'
    }

    stages {
        stage('Checkout') {
            steps {
                // Public repo, no credentials required
                git branch: 'master',
                    url: 'https://github.com/LeoRC17/gs-spring-boot.git'
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

        stage('Deploy') {
            steps {
                echo 'Deploying JAR to Nexus (snapshots)...'
                // No need for credentials here — Maven uses settings.xml
                sh 'mvn -B deploy'
            }
        }
    }
}
