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

    stage('Deploying') {
      steps {
        sh '''if sudo kubectl get pvc | grep my-httpd-pvc
then
	echo "PVC already present"
	echo "changing PVC"
	sudo kubectl apply -f  /jendata/mypvc.yml
else
	echo "Creating PVC"
	sudo kubectl create -f /jendata/mypvc.yml
fi

sleep 30

if sudo kubectl get svc | grep myserver
then
	echo "Already present, hence changing conf"
	sudo kubectl apply -f /jendata/svc.yml
else
        sudo kubectl create -f /jendata/svc.yml
fi

sleep 30

if sudo kubectl get deployment | grep mywebdeploy
then
	echo "Deployment already present, hence, rolling out"
	sudo kubectl rollout restart deployment/mywebdeploy
else
	echo "creating deployment"
	sudo kubectl create -f /jendata/Deployment.yml
fi'''
      }
    }

  }
}