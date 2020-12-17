pipeline {
  agent any
  tools {nodejs "node"}

  stages {
    stage('Install') {
      steps { sh 'npm install -g @angular/cli@next' }
    }

    stage('Test') {
      parallel {
        stage('Static code analysis') {
            steps { sh 'npm run-script lint' }
        }
        stage('Unit tests') {
            steps { sh 'npm run-script test' }
        }
      }
    }

    stage('Build') {
      steps { sh 'npm run-script build' }
    }
  }
}
