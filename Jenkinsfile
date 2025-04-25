pipeline {
	agent any
	stages {
		stage('Build Application') {
			steps {
				sh 'mvn clean package'
			}
			post {
				success {
					echo "Now Archiving the Artifacts...."
					archiveArtifacts artifacts: '**/*.war'
				}
			}
		}
		stage('Deploy stag env') {
			steps {
			build job: 'deploy_app_staging'
			}
		}
		stage('Deploy PROD env') {
			steps {
			timeout(time:5, unit:'days') {
			input message:"Approve PROD Deployment?"
			}
			build job: 'deploy_app_prod'
			}
		}
	}
} 

