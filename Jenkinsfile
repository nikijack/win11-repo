pipeline {
	agent any
	stages {
		stage('Checkout') {
			steps {
				git 'https://github.com/nikijack/win11-repo.git'
			}
		}
		stage('Maven build') {
			steps {
				bat 'mvn clean install'
			}
		}
		stage('sonarqube-analysis') {
			steps {
				withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'win11-sonar-token') {
					bat 'mvn sonar:sonar'
					echo "${currentBuild.currentResult}"
				}
			}
		}
		stage('Upload jar file to nexus') {
			when {
				expression {
					${currentBuild.currentResult} == 'SUCCESS'
				}
			}
			steps {
				nexusArtifactUploader artifacts: [
					[
						artifactId: 'win11-repo', 
						classifier: '', 
						file: 'target/win11-repo-0.1.jar', 
						type: 'jar'
					]
				],
				credentialsId: 'nexus', 
				groupId: 'com.mycompany.app', 
				nexusUrl: 'localhost:8081', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'assign-maven-snapshot', 
				version: '0.1'
			}			
		}
	}
}
