pipeline {
  agent any

  stages {
    stage('Install') {
        steps {
            // Install the ReactJS dependencies
            sh "npm install"
        }
    }
    stage('Test') {
        steps {
          // Run the ReactJS tests
          sh "npm test"
        }
    }
    stage('Checkout') {
        steps {
          // Get some code from a GitHub repository
          git branch: 'main', url: 'https://github.com/HaresMahmood/lbg-vat-calculator.git'
        }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
        steps {
            withSonarQubeEnv('sonar-qube-hares') {        
              sh "${scannerHome}/bin/sonar-scanner"
            }   
        timeout(time: 10, unit: 'MINUTES'){
            waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
