pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/theadarshsaxena/hello-world', branch: 'master', poll: true)
      }
    }

  }
}