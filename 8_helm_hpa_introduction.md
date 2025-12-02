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
 