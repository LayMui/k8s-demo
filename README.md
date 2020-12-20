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