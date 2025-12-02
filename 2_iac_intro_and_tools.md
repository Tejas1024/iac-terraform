# 2_iac_intro_and_tools.md

# 3. Introduction to IaC (Infrastructure as Code)

## What is IaC?

IaC is managing and provisioning infrastructure using configuration files instead of manually creating resources via consoles or UIs.

- Infra = servers, networks, load balancers, storage, firewalls, databases
- Code = templates/config files like `.tf`, `.yaml`, `.json`

---

## 4. Why We Need IaC?

1️⃣ Automation  
- No manual clicking in cloud console  
- Write once → deploy multiple times automatically  

2️⃣ Scalability  
- Easily create or destroy infra as needed  

3️⃣ Versioning  
- Track infra changes in Git (just like application code)  

4️⃣ Efficiency  
- Reduce time and effort during deployments  

5️⃣ Consistency  
- Same infra every time → no human mistakes  

6️⃣ Reliability  
- Predictable, repeatable deployments  

---

## 5. IaC Tools

- **Terraform** → Most popular, multi-cloud support  
- **Ansible** → Configuration automation (post-provision config)  
- **AWS CloudFormation** → AWS-only IaC  
- **Puppet** → Configuration management  
- **Chef** → Configuration management  
- **Pulumi** → IaC using programming languages (TS, Python, Go, etc.)  
- **Azure Resource Manager (ARM)** → Azure-only IaC  
- **Google Cloud Deployment Manager** → GCP IaC  
- **OpenTofu** → Open-source Terraform fork  
- **Kubernetes YAML** → Manifests defining K8s objects  
