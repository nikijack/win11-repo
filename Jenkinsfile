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
             echo "build waiting"
         }
     }
    }
}
