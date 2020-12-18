pipeline {
  agent any
  tools {nodejs "node"}

  stages {
    stage('Install') {
      steps {
        sh 'npm install karma-firefox-launcher --save-dev'
        sh 'npm install -g @angular/cli@next'
      }
    }

    stage('Test') {
      parallel {
        stage('Static code analysis') {
            steps {
              sh 'npm update'
              sh 'npm run-script lint'
            }
        }
        stage('Unit tests') {
            steps {
              sh 'npm install karma-coverage-istanbul-reporter --save-dev'
              sh 'npm run-script test'
            }
        }
      }
    }

    stage('Build') {
      steps { sh 'npm run-script build' }
    }
  }
}
