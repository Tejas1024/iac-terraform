# 11_k8s_secrets_complete.md

# 22. Kubernetes Secrets – Complete Notes

## What Are Secrets?

- Store sensitive data:
  - Username
  - Password
  - API keys
  - DB credentials
- Avoid exposing plain-text secrets in YAML.

---

## Base64 Encoding

Kubernetes Secret `data` values must be base64 encoded. [web:18][web:11]  

Encode:
echo -n "myuser" | base64

 

Decode:
echo -n "<encoded-value>" | base64 -d

 

---

## Secrets YAML Example

apiVersion: v1
kind: Secret
metadata:
name: mysecret
type: Opaque
data:
username: <base64-encoded-username>
password: <base64-encoded-password>

 

- `type: Opaque` → user-defined generic secrets [web:11][web:18]  

---

## Deployment Using Secrets

apiVersion: apps/v1
kind: Deployment
metadata:
name: secret-deployment
spec:
replicas: 3
selector:
matchLabels:
app: demo
template:
metadata:
name: pod1
labels:
app: demo
spec:
containers:
- name: con1
image: nginx
ports:
- containerPort: 80
env:
- name: PASSWORD
valueFrom:
secretKeyRef:
name: mysecret
key: password
- name: USERNAME
valueFrom:
secretKeyRef:
name: mysecret
key: username

 

- Env vars `PASSWORD` and `USERNAME` pulled from `mysecret`.

---

## Secret Commands

kubectl apply -f secret.yaml # Create secret
kubectl get secrets # List secrets
kubectl describe secret mysecret # Describe secret (no raw data)
kubectl delete secret mysecret # Delete secret

 

---

## Summary

- Secrets store sensitive values safely (base64 encoded).
- Pods consume secrets via `env.valueFrom.secretKeyRef`.
- Reusable across deployments.
- Prefer Secrets over ConfigMaps for anything confidential.  