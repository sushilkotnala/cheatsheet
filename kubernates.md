
# Kubernates
## Pod

 - Pod is the smallest entity in Kubernates environment.
 - Containers are placed inside the pods. 
 - One pod can have one or more containers.
 - Containers are executed on docker like framework which actually executes the images.

### Commands to create pod
```bash
# Create a new pod
# kubectl run <pod-name> --image=<image-name>
$ kubectl run nginx --image=nginx

# Creating pod and saving the definition intoa yaml file
# dry-run option will not actually create and start the pod
$ kubectl run nginx --image=nginx --dry-run='none' -o yaml > new.yaml

# Create a new pod form yaml file
$ kubectl create -f pod.yaml
```
#### Sample pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: first-pod
  labels:
    name: first-pod
    app: app1
spec:
  containers:
  - name: nginx
    image: nginx    
```

### List the currently running pods
```bash
kubectl get pods
```
## Edit Pods
```bash
kubectl edit pod <pod-name>
```
