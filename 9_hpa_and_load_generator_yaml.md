# 9_hpa_and_load_generator_yaml.md

# 20. HPA and Load Generator – YAML Files

## HPA YAML (hpa.yaml)

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
name: hpa
spec:
scaleTargetRef:
apiVersion: apps/v1
kind: Deployment
name: my-nginx-deployment
minReplicas: 1
maxReplicas: 10
metrics:
- type: Resource
resource:
name: cpu
target:
type: Utilization
averageUtilization: 20

text

- Target: keep average CPU at 20% of requested CPU [web:8][web:15]  
- Scales pods between 1 and 10 replicas.

---

## Load Generator YAML (load-generator.yaml)

apiVersion: apps/v1
kind: Deployment
metadata:
name: load-generator
spec:
replicas: 3
selector:
matchLabels:
app: load-generator
template:
metadata:
labels:
app: load-generator
spec:
containers:
- name: busybox
image: busybox
command:
- /bin/sh
- -c
- |
echo "Starting Load Generator...";
while true; do
wget -q -O- http://my-service.default.svc.cluster.local;
sleep 0.01;
done

text

- Continuously sends HTTP requests to `my-service` → increases CPU load.  

---

## Apply and Monitor

kubectl apply -f hpa.yaml
kubectl apply -f load-generator.yaml
kubectl get hpa

text

- `kubectl get hpa` shows current/desired replicas and CPU usage.

---

## Enable Metrics Server (Minikube)

minikube addons enable metrics-server
kubectl get all -n kube-system

text

- Required for HPA to read CPU metrics. [web:8]  