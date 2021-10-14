
## Demo app - developing with Docker
### Tutorial from [Youtube](https://www.youtube.com/watch?v=s_o8dwzRlu4&t=124s&ab_channel=TechWorldwithNana),
This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

### Following docker image will be used
#### we will be using follwoing docker image
- nanajanashia/k8s-demo-app:v1.0
- mongo:latest
- mongo-express:latest

#### We will have following parts
- load configs
- Load Secrets
- Load Deployments

### With Docker

#### To start the application

- Load Configs
	<pre><code>
	apiVersion: v1
	kind: ConfigMap
	metadata:
	  name: kube-config
	data:
	  mongo-url: mongo-service
	</code><pre>
 - Load Secrets
 	<pre><code>
	apiVersion: v1
	kind: Secret
	metadata:
	  name: kube-secret
	type: Opaque
	data:
	  mongo-user: bW9uZ291c2Vy
	  mongo-password: bW9uZ29wYXNzd29yZA==
	</code><pre>
- Load Deployment and Service
	 Refer 
	- kube.yml
	- web.yml
	- mongoexpress.yml 
- You can apply changes by
	- kubectl -f apply kube-config.yml
	- kubectl -f apply kube-secrets.yml
	- kubectl -f apply kube.yml
	- kubectl -f apply web.yml
	- kubectl -f apply mongoexpress.yml
- Access application using
			
			{ip}:30100
#### K8s commands
##### start Minikube and check status
	 minikube start --vm-driver=hyperkit 
	 minikube status
##### get minikube node's ip address
	 minikube ip
##### get basic info about k8s components
	 kubectl get node
	 kubectl get pod
	 kubectl get svc
	 kubectl get all
##### get extended info about components
	 kubectl get pod -o wide
	 kubectl get node -o wide
##### get detailed info about a specific component
	 kubectl describe svc {svc-name}
	 kubectl describe pod {pod-name}
##### get application logs
	 kubectl logs {pod-name}
  
##### stop your Minikube cluster
	 minikube stop
<br />
> :warning: **Known issue - Minikube IP not accessible** 
If you can't access the NodePort service webapp with `MinikubeIP:NodePort`, execute the following command:
  
 minikube service webapp-service
<br />
#### Links
* mongodb image on Docker Hub: https://hub.docker.com/_/mongo
* webapp image on Docker Hub: https://hub.docker.com/repository/docker/nanajanashia/k8s-demo-app
* k8s official documentation: https://kubernetes.io/docs/home/
* webapp code repo: https://gitlab.com/nanuchi/developing-with-docker/-/tree/feature/k8s-in-hour