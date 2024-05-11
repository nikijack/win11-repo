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
				sh 'mvn clean install'
			}
		}
		stage('sonarqube-analysis') {
			steps {
				withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'win11-sonar-token') {
					sh 'mvn sonar:sonar'
					echo "${currentBuild.currentResult}"
				}
			}
		}
		stage('Upload jar file to nexus') {
			when {
                		expression { currentBuild.currentResult == 'SUCCESS' }
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
				nexusUrl: 'http://35.153.18.96:8081/', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'assign-maven-snapshot', 
				version: '0.1'
			}
		}
	}
}
