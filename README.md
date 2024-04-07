# Simple Hello-World App running with Kubernetes with Horizontal Pod Autoscaling (HPA)
This is a simple Hello World app built with NodeJS.

## Installation
1. Run these commands to install the necessary tools
```
sudo apt update -y
sudo apt install git docker.io -y
sudo usermod -aG docker $USER
newgrp docker
```

## Kubernetes Setup and Running Guides

1. [Kubeadm Installation Guide](https://github.com/MohammedAtique072/kubestarter/blob/main/kubeadm_installation.md)

2. Clone the repository
```
git clone https://github.com/MohammedAtique072/nodejs-hello-world-kubernetes.git
cd nodejs-hello-world-kubernetes/k8s
```

3. Running the application
```
kubectl apply -f deployment.yml # running the application
kubectl apply -f service.yml # used to access the application
```
4. Metric server and autoscaling
```
kubectl apply -f metric-server.yml # metric server use to get the metrics about the system helps in autoscaling
kubectl autoscale deployment my-nodejs-app --cpu-percent=25 --min=1 --max=10 # horizontal pod autoscale command 
```

## Load test to increase load on cpu to check autoscale works or not

1. Download the application
```
wget https://hey-release.s3.us-east-2.amazonaws.com/hey_linux_amd64 -O hey
chmod +x hey
```

2. Running the load test
```
hey -n 100000 -c 1000 http://<ip>:<port> # of your running application
```
