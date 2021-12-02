Project code for tutorial on how to develop a Node.js/MongoDB application using Docker Compose: https://www.digitalocean.com/community/tutorials/containerizing-a-node-js-application-for-development-with-docker-compose


1) minikube start

```
mozart89@mozart89-MS-7C39:~/repos/node_project$ minikube start
😄  minikube v1.24.0 on Ubuntu 20.04
✨  Using the virtualbox driver based on user configuration
👍  Starting control plane node minikube in cluster minikube
🔥  Creating virtualbox VM (CPUs=2, Memory=3900MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.22.3 on Docker 20.10.8 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

2) eval $(minikube docker-env)

```
eval $(minikube docker-env)

```
3) docker image build

```
mozart89@mozart89-MS-7C39:~/repos/node_project$ docker build -t your_dockerhub_username/node-kubernetes .
Sending build context to Docker daemon  70.14kB
Step 1/9 : FROM node:10-alpine
...
Removing intermediate container 5681cb685cd7
 ---> 7621e2477b01
Successfully built 7621e2477b01
Successfully tagged your_dockerhub_username/node-kubernetes:latest

```

4) kubectl create

```
mozart89@mozart89-MS-7C39:~/repos/node_project$ kubectl create -f nodejs-service.yaml,nodejs-deployment.yaml,env-configmap.yaml,db-service.yaml,db-deployment.yaml,dbdata-persistentvolumeclaim.yaml,secret.yaml
service/nodejs created
deployment.apps/nodejs created
configmap/env created
service/db created
deployment.apps/db created
persistentvolumeclaim/dbdata created
secret/mongo-secret created

```

5) minikube dashboard --url #run in second terminal window

```
mozart89@mozart89-MS-7C39:~$ minikube dashboard
🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:46375/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
Opening in existing browser session.
[258816:258816:0100/000000.972445:ERROR:sandbox_linux.cc(376)] InitializeSandbox() called with multiple threads in process gpu-process.
```

6) minikube service nodejs --url

```
mozart89@mozart89-MS-7C39:~/repos/node_project$ minikube service nodejs --url
http://192.168.59.104:31556

```
