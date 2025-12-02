# 10_helm_charts_and_commands.md

# 21. Helm – Why and How

## Why Helm?

- Multiple YAMLs per app (Deployment, Service, ConfigMap, Secrets, Ingress, HPA).  
- Helm bundles them into a **Chart**:
  - Versionable
  - Reusable
  - Easy upgrade/rollback
- Ideal for:
  - Microservices
  - CI/CD deployment flows
  - Multi-environment installs (dev/stage/prod)

---

## Helm Chart Structure

- `Chart.yaml` → metadata (name, version, description)  
- `values.yaml` → default config values  
- `templates/*.yaml` → Kubernetes resource templates  

---

## Basic Helm Commands

1️⃣ Add Bitnami Repo [web:9]  
helm repo add bitnami https://charts.bitnami.com/bitnami

 

2️⃣ Search charts
helm search repo bitnami

or filter:
helm search repo bitnami | grep <template-name>

 

3️⃣ Install chart

- Auto-generated release name:
helm install bitnami/<template-name> --generate-name

 
- Custom release name:
helm install <release-name> bitnami/<template-name>

 

4️⃣ List releases
helm list

 

5️⃣ Uninstall release
helm uninstall <release-name>

 
 