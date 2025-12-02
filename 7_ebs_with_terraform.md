# 7_ebs_with_terraform.md

# 13. AWS EBS – Elastic Block Storage

## 1️⃣ EBS Volume Types (in this context)

- **Root Volume**
  - Created automatically with EC2
  - Holds OS
  - Example device names: `/dev/xvda`, `/dev/sda1`

- **Data Volume**
  - Created manually and attached to EC2
  - Example device names: `/dev/sdf`, `/dev/sdg`, `/dev/sdh` (mapped as `/dev/xvdf`, etc.)

---

## 2️⃣ EBS Size Limits (From Notes)

- **gp3** (General Purpose SSD):
  - Min 1 GiB, Max 65,536 GiB (~65 TiB)  
- **gp2**:
  - Min 1 GiB, Max 16,384 GiB (16 TiB)  

---

## 3️⃣ AZ Specific

- EBS volume **must be in same Availability Zone** as the EC2 instance.
- Example:
  - Instance-01 → `ap-south-1a`
  - Instance-02 → `ap-south-1b`
  - Volume → `ap-south-1a`  
  → Only Instance-01 can attach it.

---

## 4️⃣ Single Attachment Rule

- One EBS volume attaches to **one EC2 instance at a time** (ignoring advanced multi-attach types).
- To attach to another instance:
  - Detach from first instance
  - Attach to second

---

## 5️⃣ Terraform – Create EBS Volume

resource "aws_ebs_volume" "vol" {
availability_zone = "ap-northeast-3a"
size = 5 # GiB

tags = {
name = "vol-01"
}
}

 

---

## 6️⃣ Terraform – Attach Volume to Instance

resource "aws_volume_attachment" "ebs_att" {
device_name = "/dev/sdh"
volume_id = aws_ebs_volume.vol.id
instance_id = aws_instance.ins.id
}

 

---

## 7️⃣ Verify from EC2

Inside EC2 instance:
lsblk

 
- Shows attached disks: root + data volumes.  
 
