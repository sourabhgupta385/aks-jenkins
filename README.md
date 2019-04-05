# Azure Kubernetes Service(AKS)

To set up Kubernetes cluster on Azure using AKS, follow the steps defined in deploy_aks_cluster.txt using the Ubuntu VM.

## Deploy Jenkins on AKS

After setting up Kubernetes cluster using AKS, follow the below steps to deploy Jenkins in AKS:

### 1. Create a namespace named _jenkins_. We will create all deployment and service for jenkins in this namespace.

```
$ kubectl create ns jenkins
```

### 2. Create deployment of jenkins.

```
$ kubectl create -f jenkins-deployment.yaml --namespace=jenkins
```

### 3. To check the logs of jenkins installation, first get the pod name and then check the logs of that pod. 

```
$ kubectl get pods --namespace=jenkins
$ kubectl logs <JENKINS_POD_NAME> --namespace=jenkins --follow
```

To terminate previous command output, press Ctrl+c

### 4. Create service for jenkins deployment so that Jenkins can be accessed from web browser.

```
$ kubectl create -f jenkins-service.yaml --namespace=jenkins
```

### 5. Find the IP on which Jenkins can be accessed.

```
$ kubectl get services --namespace=jenkins
```

Previous command will give output something like below:

NAME                   TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
jenkins-service        LoadBalancer   <IP_ADDRESS>   <pending>      8080:30936/TCP   3h

If you get EXTERNAL-IP as pending, then wait for sometime and execute previous command again. You will get a IP address listed in EXTERNAL-IP.

Jenkins can be accessed on below address:

```
http://<EXTERNAL_IP_ADDRESS>:8080
```
