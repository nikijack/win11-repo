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
	}
}
