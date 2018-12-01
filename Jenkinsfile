pipeline {
	agent any
	tools {
		maven 'localMaven'
		jdk 'localJDK'
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
		stage ('Deploy to Staging'){
			steps {
				build job: 'deploy-to-staging'
			}
		}
		stage ('Deploy to Production'){
			steps {
				timeout(time:5, unit:'DAYS'){
					input message:'Approve Prod Deployment?'
				}

				build job: 'deploy-to-prod'
			}
			post {
				success {
					echo 'Code deployed to Production.'
				}

				failure {
					echo 'Deployment failed.'
				}
			}
		}
	}
}