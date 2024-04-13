pipeline {
    agent any

    stages {
      stage('Checkout') {
        steps {
          git 'https://github.com/nikijack/win11-repo.git'
        }
      }
      stage('Maven Build') {
        steps {
          sh 'mvn clean install'
        }
      }   
    }
}
