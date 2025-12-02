# 6_aws_cli_and_ssh_with_terraform.md

# 10. Connecting AWS CLI to AWS Account

## Steps

1️⃣ Login to AWS Console → **Security Credentials** under your profile.  
2️⃣ Under **Access Keys**, click **Create Access Key**.  
3️⃣ Confirm warnings → generate:
   - Access Key ID  
   - Secret Access Key (visible only once; download `.csv`).  
4️⃣ In terminal:
aws configure

text
- Enter Access Key ID  
- Secret Access Key  
- Default region (e.g. `ap-south-1`)  
- Output format (`json`)  

Now AWS CLI is authenticated to your AWS account.

---

# 11. Terraform EC2 Example

resource "aws_instance" "ins" {
ami = "ami-0938e2....."
instance_type = "t2.micro"
count = 3

tags = {
name = "ubuntu-os"
}
}

 

- Creates 3 EC2 instances, tagged `ubuntu-os`.

---

# 12. SSH Key Pair Creation Flow

1️⃣ Generate key pair:
ssh-keygen

 
- Keys stored in `~/.ssh/`  
  - Private key: `keyname`  
  - Public key: `keyname.pub`  

2️⃣ View public key:
cat <keyname>.pub

 
Copy this value.

3️⃣ Use key in Terraform:
resource "aws_key_pair" "deployer" {
key_name = "<key-pair-name>"
public_key = "<your-copied-public-key>"
}

 

- EC2 instances launched can now use this key pair for SSH access.  