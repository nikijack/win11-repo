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
				}
			}
		}
		stage('Upload jar file to nexus' {
			steps {
				nexusArtifactUploader artifacts: [
					[
						artifactId: 'win11-repo', 
						classifier: '', 
						file: 'target\\win11-repo-1.0-SNAPSHOT.jar', 
						type: 'jar'
					]
				],
				credentialsId: 'nexus', 
				groupId: 'com.mycompany.app', 
				nexusUrl: 'http://localhost:8081/', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'assign-maven-snapshot', 
				version: '1.0-SNAPSHOT'
			}
		}		
	}
}
