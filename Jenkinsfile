pipeline {
  agent {
    docker {
      image 'node'
    }

  }
  stages {
    stage('Pre Build') {
      parallel {
        stage('Print Info') {
          steps {
            sh '''node --version
ls'''
          }
        }

        stage('Clearing') {
          steps {
            sh '''rm -rf node_modules
rm -rf dist'''
          }
        }

        stage('Install npm dependencies') {
          steps {
            sh 'npm install'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'npm run build -- --base-href /angular/102/'
      }
    }

    stage('Push to Dest Repo') {
      steps {
        sh 'rm -rf node_modules'
        git(url: 'https://github.com/HamidBehnam/hamidev-mobile-dev-env-angular-dest.git', branch: 'master')
        sh '''ls
cp -a dist/hamidev-mobile-dev-env/. .
rm -rf dist
git status
git branch
git add .
git status'''
      }
    }

    stage('Post Build') {
      steps {
        sleep 10
        sh 'ls'
      }
    }

  }
  environment {
    HOME = '.'
  }
}