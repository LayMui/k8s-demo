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