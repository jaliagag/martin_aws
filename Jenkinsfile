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
    stage('debug'){
      steps {
        script {
          sh ls -l
        }
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

