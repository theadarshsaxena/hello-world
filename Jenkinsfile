pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        echo 'checkout complete'
        git(url: 'https://github.com/theadarshsaxena/hello-world', poll: true)
      }
    }

  }
}