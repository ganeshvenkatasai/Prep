```
kubectl version                        # Check installed Kubernetes version
kubectl cluster-info                   # Display cluster information
kubectl get nodes                      # List all nodes in the cluster

kubectl get pods                       # List all running pods
kubectl get pods -o wide               # List pods with detailed node information
kubectl get pods --all-namespaces      # List pods across all namespaces
kubectl describe pod <pod_name>        # Detailed information about a specific pod
kubectl delete pod <pod_name>          # Delete a specific pod

kubectl get deployments                # List all deployments
kubectl describe deployment <deployment_name>  # Get details of a specific deployment
kubectl create deployment <name> --image=<image>  # Create a deployment
kubectl scale deployment <name> --replicas=<count>  # Scale a deployment
kubectl delete deployment <deployment_name>  # Delete a deployment

kubectl get services                   # List all services
kubectl describe service <service_name>  # Get details of a specific service
kubectl expose deployment <name> --type=LoadBalancer --port=80  # Expose a deployment as a service
kubectl delete service <service_name>   # Delete a service

kubectl get namespaces                 # List all namespaces
kubectl create namespace <namespace_name>  # Create a new namespace
kubectl delete namespace <namespace_name>  # Delete a namespace

kubectl get configmaps                 # List all ConfigMaps
kubectl create configmap <name> --from-literal=key=value  # Create a ConfigMap
kubectl delete configmap <name>         # Delete a ConfigMap

kubectl get secrets                    # List all secrets
kubectl create secret generic <name> --from-literal=key=value  # Create a secret
kubectl delete secret <name>            # Delete a secret

kubectl apply -f <file.yaml>           # Apply changes from a YAML file
kubectl delete -f <file.yaml>          # Delete resources defined in a YAML file
kubectl logs <pod_name>                # View logs of a pod
kubectl exec -it <pod_name> -- /bin/sh  # Access a running container inside a pod

kubectl get events                     # View cluster events
kubectl top nodes                       # Show CPU and memory usage of nodes
kubectl top pods                        # Show CPU and memory usage of pods
kubectl drain <node_name>               # Safely remove a node for maintenance
kubectl cordon <node_name>              # Mark a node as unschedulable
kubectl uncordon <node_name>            # Mark a node as schedulable again


### Kubernetes Deployment YAML ###
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: my-app:latest
          ports:
            - containerPort: 80

---

### Kubernetes Service YAML ###
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

---

### Kubernetes ConfigMap YAML ###
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  namespace: default
  labels:
    app: my-app
data:
  APP_ENV: "production"
  LOG_LEVEL: "debug"

---

### Kubernetes Secret YAML ###
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  namespace: default
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQ=  # Base64 encoded password

---

### Kubernetes Persistent Volume (PV) YAML ###
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"

---

### Kubernetes Persistent Volume Claim (PVC) YAML ###
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

---

### Kubernetes Ingress YAML ###
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app-service
                port:
                  number: 80

```
