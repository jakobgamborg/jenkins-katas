pipeline {
  agent any
  stages {
    stage('clone down'){
      steps{
        stash(exludes: '.git', name: 'code')
      }
    }

    stage('Parallel execution') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('Build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }
          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            sh 'ls'
            deleteDir()
            sh 'ls'  
            unstash 'code'
          }
          options {
            skipDefaultCheckout()
          }
        }


      }
    }

  }
  environment {
    Hello = ''
  }
}