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
             sh 'mvn clean install -Dmaven.repo.local=C:\ProgramData\Jenkins\.jenkins\workspace\assign-cd-pipeline'
         }
     }
    }
}
