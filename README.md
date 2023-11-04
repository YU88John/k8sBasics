# Kubernetes Basics - Mini Project 

### Prerequisites

1. A working single or multi-node Kuberentes cluster. <br>
   You can use a cloud kubernetes setup or local minikube. However, minikube is sufficient for this mini project. <br>
   If your local machine doesn't have minikube, please follow the installations steps via: https://minikube.sigs.k8s.io/docs/start/
2. Docker

This is a simple project built using Kubernetes. 

There are two setups:
1. "Hello World" app 
2. "Hello World" app with nginx redirection using `/nginx`

### Setup the environment

**1. Clone the repository**

`git clone https://github.com/YU88John/k8sBasics.git`

**2. Create minikube cluster**

`minikube start --memory 4096` <br>
In certain devices, there is a virtualization error displaying "Enabling VT-X AMD-v in the BIOS is mandatory." If you have similar problem, please proceed with this command instead `minikube start --memory 4096 --driver=virtualbox --no-vtx-check`. <br>
Ensure the cluster is running without any problems `minikube status`.

**3. Build Docker image for both deployments**

This step is optional. You can directly deploy definition files which contain my public image. <br>
If you wish to build your own image, you can do this step.

`docker login` Enter the username and password of your Docker Hub <br>
Go into k8s-web-hello directory `cd /k8s-web-hello` <br>
Build the image with your desired name `docker build -t <YOUR_IMAGE>:v1 .` <br>
Tag your image with the repository name `docker tag <YOUR_IMAGE>:v1 <YOUR_REPO>/<YOUR_IMAGE>:v1` <br>
Push the image to your repository `docker push <YOUR_REPO>/<YOUR_IMAGE>:v1` <br>

Repeat the same steps for `k8s-web-to-nginx` image. Replace the placeholders with your actual values.

**4. Deploy the services**

If you want to experience more about kubernetes components, apply them separately. Otherwise, you can directly apply all-in-one definition files.

`kubectl apply -f k8s-web-hello` <br>
`kubectl apply -f k8s-web-to-nginx`

**5. Access the service**

Ensure all the components are up and running `kubectl get all`. <br>
Open the deployment in the browser `minikube service k8s-web-to-nginx`




