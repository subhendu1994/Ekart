pipeline {
    agent any

    // Define tools to be used in this pipeline
    tools {
      maven 'Maven'
          // Set environment variables
    environment {
        SCANNER_HOME = tool 'sonar'
    }  
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
      stage('Sonarqube') {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar-cred') {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Shopping-Cart \
                   -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=Shopping-Cart '''
               }
            }
        }  
   
    
    }
}
    
