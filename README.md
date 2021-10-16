# kubectl


# [Kubernetes] deployment from docker Registry ( AutoGenerate YAML for Deployment )

```powershell
# read the manual for options
kubectl create deployment NAME --image=image [--dry-run] [options]
kubectl create deployment --help
# =========================================================


# YAML AutoGenerate Deployment directly from image registry
# Creating YAML manifests from scratch is time-consuming and error-prone !!
kubectl create deployment kursus-app-2020 --image=jalalhejazi/angular-kursus-2020:latest

# Get Deploy
kubectl get deploy

# port forwarding 
kubectl port-forward deployment/kursus-app-2020 8888:80

# cleanup
kubectl delete deployment kursus-app-2020
```


## Create deployment.yaml from docker image:

```powershell
# Dry-Run Before running --> Generate yaml deployment from image to 
# be used in kubectl apply -f deployment.yaml 

kubectl create deployment kursus-app-2020 --image=jalalhejazi/angular-kursus-2020 --output='yaml'  --dry-run >>  deployment.yaml

# Create/Update Deployment from yaml file
kubectl apply -f deployment.yaml

## deployment.apps/kursus-app-2020 created
## deployment.apps/kursus-app-2020 configured

# port forwarding 
kubectl port-forward deployment/kursus-app-2020 8888:80
```

# deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: kursus-app-2020
  name: kursus-app-2020
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kursus-app-2020
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: kursus-app-2020
    spec:
      containers:
      - image: jalalhejazi/angular-kursus-2020
        name: angular-kursus-2020
        resources: {}
status: {}
```

# Manual-Scaling 

```powershell
kubectl scale --replicas=2 deployment/kursus-app-2020
kubectl scale --replicas=4 deployment/kursus-app-2020
```

# Auto-Scaling
Assuming horizontal Pod autoscaling is enabled in your cluster, you can setup an autoscaler for your Deployment and choose the minimum and maximum number of Pods you want to run based on the CPU utilization of your existing Pods.

```powershell
kubectl autoscale deployment/kursus-app-2020 --min=1 --max=4 --cpu-percent=80
```



<br>
<hr>
