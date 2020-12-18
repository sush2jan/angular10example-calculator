pipeline {
  agent any
  tools {nodejs "node"}

  stages {
    stage('Install') {
      steps {
        sh 'npm install -g @angular/cli@next'
      }
    }

//   stage('Test') {
//      parallel {
//        stage('Static code analysis') {
//            steps {
//              sh 'npm update'
//              sh 'npm run-script lint'
//            }
//        }
//        stage('Unit tests') {
//            steps {
//              sh 'export CHROME_BIN=/snap/bin/chromium'
//              sh 'npm run-script test'
//            }
//        }
//      }
//    }

    stage('Build') {
      steps {
        sh """
          cd ${WORKSPACE}
          ng build --prod
          if [ -d dist ]
          then
              aws s3 cp dist s3://pm-ansible-ui-app-bucket --acl public-read --recursive
              aws cloudfront create-invalidation --distribution-id EUQ73ZEC9O6F1 --paths "/*"
          else
              echo “dist folder not found”
          exit 1
          fi
        """
      }
    }
  }
}
