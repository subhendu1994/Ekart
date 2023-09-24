pipeline {
    agent any

    // Define tools to be used in this pipeline
    tools {
      maven 'Maven'
    }
    
    stages {
     // Stage 1: Git Checkout
      stage('Git Checkout') {
        steps {
        // Check out the 'main' branch from the specified Git repository
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/subhendu1994/Ekart.git']])
        }
      }
    
      // Stage 2: Compile
      stage('Compile') {
        steps {
        // Clean and compile the project using Maven, skipping tests
          sh "mvn clean compile -DskipTests=true"
        }
      }    
      stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
    }
}
    
