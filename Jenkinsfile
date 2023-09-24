pipeline {
    agent any

    stages {
     // Stage 1: Git Checkout
      stage('Git Checkout') {
        steps {
        // Check out the 'main' branch from the specified Git repository
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/subhendu1994/Ekart.git']])
        }
      }
    }
}
    
