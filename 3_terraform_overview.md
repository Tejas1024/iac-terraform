# 3_terraform_overview.md

# 6. Terraform – Overview

## What is Terraform?

- Open-source IaC tool developed by HashiCorp [web:1][web:2][web:4][web:5][web:12]  
- Lets you define infrastructure using code and manage it safely and efficiently [web:3][web:4][web:12]  
- Supports multiple providers: AWS, Azure, GCP, Kubernetes, VMware, GitHub, etc. [web:5][web:12]  
- Uses a declarative configuration language:
  - HCL → HashiCorp Configuration Language [web:5][web:12]

---

## History of Terraform

- Created by HashiCorp (founded by Mitchell Hashimoto and Armon Dadgar) [web:6][web:13][web:20]  
- First production version released in July 2014 [web:6][web:20]  

---

## Features of Terraform

1️⃣ Multi-cloud support (AWS, Azure, GCP, on‑prem, etc.) [web:5][web:12]  
2️⃣ Declarative language (HCL) → describe desired state, Terraform figures out how [web:3][web:4][web:12]  
3️⃣ Free and open-source CLI [web:2][web:5][web:19]  
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
