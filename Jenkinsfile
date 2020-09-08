pipeline {
  agent any
  stages {
    stage('CheckOut') {
      parallel {
        stage('CheckOut') {
          steps {
            git(url: 'https://github.com/theadarshsaxena/hello-world', branch: 'master')
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


if sudo kubectl get deployment | grep mywebdeploy
then
	echo "Deployment already present, hence, rolling out"
	sudo kubectl rollout restart deployment/mywebdeploy
else
	echo "creating deployment"
	sudo kubectl create -f /jendata/deployment.yml
fi

sleep 10

if sudo kubectl get svc | grep mywebdeploy
then
	echo "Already present"
else
        sudo kubectl expose deployment mywebdeploy --type=LoadBalancer
fi
'''
      }
    }

    stage('Testing') {
      steps {
        sh '''cd /jendata
status=$(sudo curl -o /dev/null -s -w "%{http_code}" $(sudo kubectl get all | sudo awk \'/LoadBalancer/ {print $4}\'))
if status==200
then
    echo "everything running fine"
else
    echo "not fine"
    exit 1
fi'''
        echo 'Everything fine'
      }
    }

  }
}