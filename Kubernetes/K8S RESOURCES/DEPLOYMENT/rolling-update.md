# Topic: Rolling Update & Rollback Deployment Strategy
- Date: 15-12-25
---
````
apiVersion: apps/v1 
kind: Deployment
metadata: 
  name: studentapp

spec: 
  replicas: 1
  selector: 
   matchLabels:
     app: studentapp

  template: 
   metadata:
      name: tmp-1
      labels:
        app: studentapp
   spec: 
     containers:
      - name: c2 
        image: abhipraydh96/studentapp:v1
        ports:
        - containerPort: 80
---
apiVersion: v1 
kind: Service 
metadata:
  name: svc-studentapp
spec:
  selector:
    app: studentapp
  ports:
   - protocol: "TCP"
     port: 80
     targetPort: 80
  type: NodePort
````

````
kubectl get deploy
````
````
kubectl get svc
````
## v1 
<img width="1558" height="447" alt="image" src="https://github.com/user-attachments/assets/ae9afa5d-103c-4943-b044-1153b2b974d2" />

## Rolling Update
- switch to newer version
````
kubectl get deploy -o wide
````
````
kubectl set image deploy/studentapp  c2=abhipraydh96/studentapp:v2 --record
````
````
kubectl rollout history deploy/studentapp
````
## v2
<img width="641" height="613" alt="image" src="https://github.com/user-attachments/assets/72e45cfa-2b71-4ec3-b551-7694b3e1aa32" />


## rollback to previous version
````
kubectl rollout undo deploy/studentapp
````
---
