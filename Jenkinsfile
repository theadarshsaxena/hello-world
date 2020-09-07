pipeline {
  agent any
  stages {
    stage('CheckOut') {
      parallel {
        stage('CheckOut') {
          steps {
            sh '''pwd
sudo cp -r -v -f * /jendata'''
          }
        }

        stage('Debug') {
          steps {
            sh '''if ls /jendata | grep hello-world.txt
then
  exit 1
else
  exit 0
fi'''
          }
        }

      }
    }

  }
}