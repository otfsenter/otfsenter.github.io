# k8s


## tutorial address: 1:16:19

https://www.youtube.com/watch?v=X48VuDVv0do&t=6211s


## insall minikube

```
brew update
brew install hyperkit
brew install minikube

brew install docker-machine-driver-hyperkit
sudo chown root:wheel /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit
sudo chmod u+s /usr/local/opt/docker-machine-driver-hyperkit/bin/docker-machine-driver-hyperkit

minikube start --vm-driver=hyperkit

minikube status
kubectl version
kubectl get nodes
kubectl get pod
kubectl get service
```

## create deployment

```
kubectl create deployment -h
kubectl create deployment nginx-deploy --image=nginx
kubectl get deployment
kubectl get replicaset
kubectl get node

kubectl edit deployment nginx-deploy

kubectl create deployment mongo-depl --image=mongo
kubectl describe pod mongo-depl-5fd6b7d4b4-8qxpz
kubectl logs mongo-depl-5fd6b7d4b4-8qxpz
kubectl exec -it mongo-depl-5fd6b7d4b4-8qxpz -- bin/bash

kubectl delete deployment nginx-deploy
kubectl delete deployment mongo-depl
```


## create deployment from yaml file

```
kubectl apply -f nginx-deployment.yaml
```

nginx-deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        ports:
        - containerPort: 8080
```


nginx-service.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocal: TCP
      port: 80
      targetPort: 8080
```

**get service status**
```
kubectl get service
kubectl describe service nginx-service
```

**get ip**

```
kubectl get pod -o wide
```

**get actual nginx-deployment yaml file**

```
kubectl get deployment nginx-deployment -o yaml
```

**delete deployment and service after test**

```
kubectl delete -f nginx-deployment.yaml 
kubectl delete -f nginx-service.yaml 
```


## 阿里云镜像源安装K8S

https://zhuanlan.zhihu.com/p/59048502


## 从零开始部署k8s

https://www.vickey-wu.com/posts/deploy-k8s-by-kubeadm/
