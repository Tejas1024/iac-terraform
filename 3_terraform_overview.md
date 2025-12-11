# 3_terraform_overview.md

# 6. Terraform – Overview

## What is Terraform?

- Open-source IaC tool developed by HashiCorp   
- Lets you define infrastructure using code and manage it safely and efficiently   
- Supports multiple providers: AWS, Azure, GCP, Kubernetes, VMware, GitHub, etc.   
- Uses a declarative configuration language:
  - HCL → HashiCorp Configuration Language 

---

## History of Terraform

- Created by HashiCorp (founded by Mitchell Hashimoto and Armon Dadgar)   
- First production version released in July 2014   

---

## Features of Terraform

1️⃣ Multi-cloud support (AWS, Azure, GCP, on‑prem, etc.)   
2️⃣ Declarative language (HCL) → describe desired state, Terraform figures out how   
3️⃣ Free and open-source CLI   
4️⃣ State management via `terraform.tfstate`  
5️⃣ Plan & apply mechanism:
   - `terraform plan` → preview changes  
   - `terraform apply` → execute changes  
6️⃣ Supports modules (reusable infra building blocks)  

---

## Common Terraform Objects

- **Resources** → EC2, VPC, S3, RDS, etc.  
- **Variables** → Parameterize values  
- **Outputs** → Expose info like IPs, IDs  
- **Providers** → Bridge between Terraform and specific platforms  
