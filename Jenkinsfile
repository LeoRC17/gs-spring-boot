pipeline {
	agent {
		docker {
			image 'maven:3.8.6-openjdk-17'
		}
	}

    	stages {
        	stage('Checkout') {
            		steps {
               			git url: 'https://github.com/LeoRC17/gs-spring-boot.git', branch: 'master'
            	}
        }

        stage('Build') {
        	steps {
                	echo 'Building fat JAR...'
                		sh 'mvn clean compile assembly:single'
            	}
        }

        stage('Test') {
        	steps {
                	echo 'Running tests...'
                	sh 'mvn test'
            	}
        }

        stage('Archive') {
        	steps {
                	archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            	}
        }
    }
}
