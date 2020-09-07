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
	sudo kubectl apply -f  /webserver/mypvc.yml
else
	echo "Creating PVC"
	sudo kubectl create -f /webserver/mypvc.yml
fi

if sudo kubectl get svc | grep myserver
then
	echo "Already present, hence changing conf"
	sudo kubectl apply -f /webserver/svc.yml
fi

if sudo kubectl get deployment | grep mywebdeploy
then
	echo "Deployment already present, hence, rolling out"
	sudo kubectl rollout restart deployment/mywebdeploy
else
	echo "creating deployment"
	sudo kubectl create -f /webserver/Deployment.yml
fi'''
      }
    }

    stage('Testing') {
      steps {
        sh '''status=$(curl -o /dev/null -s -w "%{http_code}" $(siteaddress))
if ($status == 200)
then
    echo "everything running fine"
    exit 0
else
    echo "problem found with error status code: $status"
fi



'''
      }
    }

  }
}