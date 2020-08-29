pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/theadarshsaxena/hello-world', poll: true)
      }
    }

  }
}