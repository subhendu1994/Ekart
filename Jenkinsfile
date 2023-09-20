pipeline {
    agent any
    
    tools{
        jdk  'java'
        maven  'Maven'
    }
    
    environment{
        SCANNER_HOME= tool 'Sonar'
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/subhendu1994/Ekart.git']])
            }  
        }
          
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=true"
            }
        }
   
    }   
    }
