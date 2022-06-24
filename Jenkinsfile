pipeline {
  agent any

  stages {
    stage('clean workspace'){
      steps {
        cleanWs()
        }
      }
    stage('checkou'){
      steps {
        checkout scm
      }
    }
    stage('terraform'){
      steps {
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

