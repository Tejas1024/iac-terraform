# 8_helm_hpa_introduction.md

# 14. Helm – Basic Workflow

## Create Own Helm Chart

1️⃣ Create chart:
helm create hart-name>

 

2️⃣ Package chart:
helm package hart-name>

 

3️⃣ Create repo index (for hosting your own chart repo):
helm repo index .

 

4️⃣ Install chart:
helm install <release-name> hart-name>



---

# 15. Why Helm?

- Bundle many YAMLs (Deployment, Service, ConfigMap, Secrets, HPA, etc.) into a single **chart**.  
- Simplifies updates and rollbacks:
  - `helm upgrade`
  - `helm rollback`  
- Great for CI/CD and multi-environment deployments.

---

# 16. Horizontal Pod Autoscaler (HPA) – Concept

- HPA automatically adjusts the number of pods based on metrics (e.g., CPU). [web:8][web:15]  
- Example logic:
  - If CPU usage above target → scale up
  - If CPU usage below target → scale down  

---

# 17. Deployment YAML with CPU Resources

apiVersion: apps/v1
kind: Deployment
metadata:
name: my-nginx-deployment
labels:
app: nginx
spec:
replicas: 1
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: con1
image: shanthappu/static-web-host:v1
ports:
- containerPort: 80
resources:
limits:
cpu: 500m
requests:
cpu: 50m

text

- `requests.cpu` → minimum CPU for scheduling  
- `limits.cpu` → max CPU allowed per pod  

---

# 18. Service YAML (for that Deployment)

apiVersion: v1
kind: Service
metadata:
name: my-service
spec:
selectors:
app: nginx
ports:
- name: load-balancer
protocol: TCP
port: 80
targetPort: 80

text

- `selector` must match pod labels  
- `port` = service port  
- `targetPort` = container port  

---

# 19. Port Forward Example

kubectl port-forward svc/my-service 8085:80 --address=0.0.0.0

text

- Access app at: `http://localhost:8085`  
text
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