# 4_terraform_architecture.md

# 7. Terraform Architecture (Diagram Explanation)

## High-Level Flow

**Config File (.tf)** → **Terraform Core** → **Providers** → **Cloud Output**

---

## Configuration File

Content examples:

- Key pair configuration  
- Storage (S3)  
- EC2 instance definitions  
- VPC configuration  
- IAM roles and policies  

These live in `.tf` files and describe desired infrastructure.

---

## Terraform Core

Responsibilities:

- Read `.tf` configuration files  
- Parse and validate config  
- Compute the execution plan  
- Communicate with providers  
- Maintain state (desired vs. actual)  

Terraform Core does not directly talk to AWS/Azure; it works through **providers**. [web:3][web:4][web:12]

---

## Providers and Plugins

- AWS, Azure, GCP, Kubernetes, VMware, GitHub, etc. [web:5][web:12]  
- Handle:
  - Authentication
  - CRUD for resources
  - Reading remote state  
- **Backends**:
  - Local backend → state in local files
  - Remote backend → state in S3, GCS, etc.

---

## Apply Phase – Cloud Output

- `terraform apply` compares:
  - Desired state (config)
  - Current state (state file + real cloud)
- Then:
  - Creates EC2 instances, VPC, S3, IAM, etc.
  - Updates `terraform.tfstate`
- Outputs (e.g. public IP) can be printed via `output` blocks.  
