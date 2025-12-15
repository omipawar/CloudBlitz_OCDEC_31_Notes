# Topic: Deployment
- Date: 12-12-25
---

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployement
spec:
  replicas: 3
  selector:
    matchLabels:
        app: gaming
  template:
    metadata:
      name: tmp-01
      labels:
         app: gaming
    spec:
      containers:
         - name: super-mario
           image: abhipraydh96/super-mario
           ports:
             - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: svc-gaming
spec:
 selector:
    app: gaming
 ports:
   - port: 80
     targetPort: 80
     protocol: "TCP"
 type: NodePort
 ```

#### Commands:
````
kubectl get deploy
````
````
kubectl get svc
````
