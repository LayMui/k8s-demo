# Steps
1. kubectl apply -f secrets.yaml
2. kubectl get secret
```
NAME                  TYPE                                  DATA   AGE
default-token-prpr6   kubernetes.io/service-account-token   3      3h44m
mongodb-secret        Opaque                                2      8s
```

3. kubectl apply -f mongodb-deployment.yaml
deployment.apps/mongodb-deployment created

4. kubectl get all
```
NAME                                     READY   STATUS                       RESTARTS   AGE
pod/mongodb-deployment-ffb479dbc-dvbdk   0/1     CreateContainerConfigError   0          26s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3h48m

NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/mongodb-deployment   0/1     1            0           26s

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/mongodb-deployment-ffb479dbc   1         1         0       26s
```
