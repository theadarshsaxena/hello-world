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
  echo "success"
else
  exit 1
fi'''
          }
        }

      }
    }

    stage('error') {
      steps {
        echo 'Success'
      }
    }

  }
}