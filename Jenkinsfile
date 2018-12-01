pipeline {
	agent any
	tools {
		maven 'Maven 3.6.0'
		jdk 'jdk8'
	}
	stages{
		stage('Build'){
			steps {
				bat 'mvn clean package'
			}
			post {
				success {
					echo 'Now archiving...'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
	}
}

