pipeline {
    agent any

    // Define tools to be used in this pipeline
    tools {
        maven 'Maven'
    }

    // Set environment variables
    environment {
        SCANNER_HOME = tool 'Sonar'
    }

    // Define the stages of the pipeline
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

        // Stage 3: OWASP Scan
        stage('OWASP Scan') {
            steps {
                // Run an OWASP Dependency-Check scan on the project
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
          stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('sonar') {
                   sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Shopping-Cart \
                   -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=Shopping-Cart '''
               }
            }
        }
            stage('Deploy To Nexus') {
           steps {
               withMaven(globalMavenSettingsConfig: 'global-xml') {
               sh "mvn deploy -DskipTests=true"
        
               }
          
           }
       } 
    }
}
