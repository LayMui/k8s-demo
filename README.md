# Steps
0. To create a cluster
```
minikube start --vm-driver=hyperkit
```
1. kubectl apply -f mongo-secret.yaml
2. kubectl get secret
```
NAME                  TYPE                                  DATA   AGE
default-token-prpr6   kubernetes.io/service-account-token   3      3h44m
mongodb-secret        Opaque                                2      8s
```

3. kubectl apply -f mongodb-deployment.yaml

4. kubectl get all

5. kubectl get pod 

   kubectl get pod --watch 

   kubectl describe pod <pod-name>

6. kubectl get pod 
```
NAME                                 READY   STATUS    RESTARTS   AGE
mongodb-deployment-8f6675bc5-5k5dl   1/1     Running   0          3m4s
```

# Create an internal service

Allow you to put multiple documents in 1 file
--- denote separation of documents
Put Deployment & Service in 1 file because they belong together

kubectl apply -f mongodb-deployment.yaml

kubectl get service
```
NAME              TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)     AGE
kubernetes        ClusterIP   10.96.0.1      <none>        443/TCP     4h14m
mongodb-service   ClusterIP   10.97.167.20   <none>        27017/TCP   11s
```

kubectl describe service mongodb-service
```
Name:              mongodb-service
Namespace:         default
Labels:            <none>
Annotations:       kubectl.kubernetes.io/last-applied-configuration:
                     {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"mongodb-service","namespace":"default"},"spec":{"ports":[{"port":...
Selector:          app=mongodb
Type:              ClusterIP
IP:                10.97.167.20
Port:              <unset>  27017/TCP
TargetPort:        27017/TCP
Endpoints:         172.17.0.4:27017
Session Affinity:  None
Events:            <none>
```

IP address of the Pod = 172.17.0.4 and port is 27017 where the app is listening to

kubectl get pod -o wide 

kubectl get all  -> to show ALL components

kubectl get all | grep mongodb -> to filter by monddb


Need to tell mongoexpress which database to connect?
MongoDB Address/Internal Service

which credentials to authenticate?

kubectl apply -f mongo-configmap.yaml

kubectl apply -f mongoexpress-deployment.yaml

kubectl get pod

kubectl logs mongo-express-78fcf796b8-9glzp
```
Waiting for mongodb-service:27017...
Welcome to mongo-express
------------------------


Mongo Express server listening at http://0.0.0.0:8081
Server is open to allow connections from anyone (0.0.0.0)
basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!
Database connected
Admin Database connected
```

To access mongo express from a browser, we need a external service
Add the service to the mongoexpress-deployment.yaml
How to make it an External Service?
 - type: "LoadBalancer"
 ..assigns service an external IP address and so accepts external requests
 
 - nodePort: Port where the external IP address will be opened 
   It is the Port you put in the browser to access this service
   must be between 30000 - 32767

kubectl get service
```
NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes              ClusterIP      10.96.0.1      <none>        443/TCP          7h32m
mongo-express-service   LoadBalancer   10.96.62.211   <pending>     8081:30000/TCP   7m9s
mongodb-service         ClusterIP      10.97.167.20   <none>        27017/TCP        3h18m
```

Internal Service or Cluster IP is DEFAULT
Cluster IP will give the service an internal IP address which is 10.97.xx
LoadBalancer will also give the service an internal IP address and in additional an external IP

minikube service mongo-express-service to access the external IP address

# To setup namespace
brew install kubectx

```
kubens
```

# How to install ingress controller in minikube
```
minikube addons enable ingress
```
automatically starts the K8s Nginx implementation of Ingress Controller


kubectl get pod -n kube-system
You will see the Nginx ingress controller running in your cluster
```
NAME                                        READY   STATUS      RESTARTS   AGE
coredns-f9fd979d6-ptjz5                     1/1     Running     1          24h
etcd-minikube                               1/1     Running     1          25h
ingress-nginx-admission-create-dxd8m        0/1     Completed   0          6m22s
ingress-nginx-admission-patch-frrkl         0/1     Completed   0          6m22s
ingress-nginx-controller-558664778f-8gwlp   1/1     Running     0          6m22s
kube-apiserver-minikube                     1/1     Running     1          25h
kube-controller-manager-minikube            1/1     Running     1          25h
kube-proxy-pf5dj                            1/1     Running     1          24h
kube-scheduler-minikube                     1/1     Running     1          25h
storage-provisioner                         1/1     Running     8          25h
```




