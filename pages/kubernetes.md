# minikube
it is a lightweight tool that let us run kubernetes cluster locally.
```
minikube start
```
# kubectl
it is the command line used to interact with kubernetes clusters.
all of the kubectl commands can be found in [this doc](https://kubernetes.io/docs/reference/kubectl/generated/). check also [this doc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) for a better gui of commands.
here you can find the essential commands to run to manage k8s.
## check running cluster
```sh
kubectl cluster-info
```
## run a pod
```sh
kubectl run myfirstpod --image=hello-world:latest --port=80
```
## list running pods
```sh
kubectl get pods
```
## pod logs
```sh
kubectl logs <pod_name>
```
## get
### configmap
```sh
kubectl get configmaps -A -o yaml
```
### pods detailed information
```
kubectl describe pod <pod_name>
```
### labels
```sh
kubectl get pods --selector app=httpd-server --show-labels
kubectl lots -l app=httpd-serve
```
### namespaces
```sh
kubectl get namespaces
```
## create
### namespace
```sh
kubectl create namespace <new_namespace>
```
## port forwarding
redirect a host port to a container port. 
```
kubectl port-forward pod/httpd-server 8080:80
```
## apply
apply a configuration to a resource by file name or stdin.
```sh
kubectl apply -f httpd-server-deployment.yml  
```
## set
to update an image version
```sh
kubectl set image deployments/rollingapp-deployment nginx-hello=nginxdemos/hello:plain-text
```

## delete a pod
```sh
kubectl delete pods myfirstpod
```
## delete a deployment
```sh
kubectl delete deployment mydeployment
```
delete a service
```sh
kubectl delete service myservice
```

## force delete pv
You can delete the PV using following two commands:

```sh
kubectl delete pv <pv_name> --grace-period=0 --force
```

And then deleting the finalizer using:

```sh
kubectl patch pv <pv_name> -p '{"metadata": {"finalizers": null}}'
```

# notes
- k8s relies on container mechanism (e.g. docker)
- context: a container is highly linked to the kernel so it has no view of what is happening outside this kernel thus on the host machine.
- k8s then brings container orchestration and management on server clusters. k8s take charge of several kernels so then it can manage containers on these host linux servers (physical or virtual or located in private or public cloud). 
- the orchestration can:
	- create applicative services (frontend/backend)
	- plan their execution in a cluster
	- guaranty their integrity
	- guaranty monitoring
- with k8s, the user do not have to take care of the VM management anymore.
# deployments
[deployment doc](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
## manifest example
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: rollingapp-deployment
	namespace: default
	labels:
		app: rollingapp
spec:
	selector:
		matchLabels:
		app: rollingapp
	replicas: 1
	strategy:
		rollingUpdate:
			maxSurge: 25%
			maxUnavailable: 25%
		type: RollingUpdate
	template:
		metadata:
			labels:
			app: rollingapp
		spec:
			containers:
			- name: nginx-hello
			  image: nginxdemos/hello:latest
			  ports:
			  - containerPort: 80
```
# services
## Load balancer service
### manifest example
#### service with port 80 and target port 80
```yml
apiVersion: v1
kind: Service
metadata:
	name: mws-service
	labels:
	app: mywebserver
spec:
	type: LoadBalancer
	ports:
		- name: http
		port: 80
		protocol: TCP
		targetPort: 8080
	selector:
		app: mywebserver
	sessionAffinity: None
```
# configmap
ConfigMaps are a Kubernetes mechanism that let you inject configuration data into application [pods](https://kubernetes.io/docs/concepts/workloads/pods/).
## example configmap
```sh
kind: ConfigMap
	apiVersion: v1
	metadata:
		name: motd-config
		namespace: default
		labels:
			app: motd
data:
	MESSAGE: "Hi i'm a simple container inside a pod"
	OTHER_MESSAGE: "You can't see me!"
```
apply and display configmap
```sh
kubectl apply -f motd-deployment.yml
kubectl apply -f motd-config.yml
kubectl get configmaps -A -o yaml
```
# storage
Ways to provide both long-term and temporary storage to Pods in your cluster.
## persistent volume and volume claim example
```yaml
kind: PersistentVolume
apiVersion: v1
metadata:
  name: mydatabase-pv
  labels:
    app: mydatabase
spec:
  storageClassName: manual
  capacity:
    storage: 5M
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/mydatabase"
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mydatabase-pvc
  labels:
    app: mydatabase
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 5M
```