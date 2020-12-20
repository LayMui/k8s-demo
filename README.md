# Steps
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

   kubetcl get pod --watch 

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

kubectl apply -f -f mongodb-deployment.yaml

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