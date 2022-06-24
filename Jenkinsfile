pipeline {
  agent any

  stages {
    stage('clean workspace'){
      steps {
        cleanWs()
        }
      }
    stage('checkout'){
      steps {
        checkout scm
      }
    }
    stage('terraform'){
      steps {
        ls -l
        sh './terrformw apply -auto-approve -no-color'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }

}

