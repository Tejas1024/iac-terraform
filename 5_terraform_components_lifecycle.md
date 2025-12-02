# 5_terraform_components_lifecycle.md

# 8. Components of Terraform

## 1️⃣ Terraform Core

- Reads configuration files  
- Manages the state file  
- Builds the execution plan  
- Coordinates providers to reach desired state  

---

## 2️⃣ Providers

- Plugins to interact with cloud/API:
  - AWS, Azure, GCP, Kubernetes, GitHub, VMware, etc.  
- Authenticate and perform create/update/delete on resources  
- Initialized via:
terraform init

text

---

## 3️⃣ Provisioners

- Run scripts or commands **after** resources are created:
- Install software on EC2
- Configure files
- Used sparingly in real projects; config management tools (Ansible, etc.) are preferred.

---

## 4️⃣ Terraform State

- Stored typically in `terraform.tfstate`  
- JSON format  
- Tracks:
- What resources exist
- IDs and metadata
- Dependencies  
- Critical for:
- Incremental updates
- Detecting drift
- Safe refactors

---

# 9. Terraform Lifecycle (Init → Plan → Apply → Destroy)

1️⃣ **Initialization**
terraform init

 
- Downloads providers/plugins  
- Initializes backend (state storage)  

2️⃣ **Planning**
terraform plan

 
- Validates configuration  
- Shows which resources will be created/changed/destroyed  

3️⃣ **Apply**
terraform apply

 
- Executes plan  
- Provisions/updates/destroys resources  
- Updates state file  

4️⃣ **Destroy**
terraform destroy

 
- Removes all resources defined in current config  
- Cleans infra (helps avoid extra cloud cost) 