# 🛡️ AWS IAM Role Lab  
**Securely delegate access across your AWS services like a pro**

[![Made by Charles Bucher](https://img.shields.io/badge/Made%20By-Charles%20Bucher-blue)](https://github.com/Tommy813-lab)

---

## 📚 Scenario

> “I have an EC2 instance that needs to talk to S3, but I don’t want to hardcode AWS credentials. What do I do?”

You use **IAM Roles**—that’s what.

This lab simulates a real-world support ticket:

💬 _“Hey Charles, the EC2 instance can't access the S3 bucket. Do I just paste in the access keys?”_

🚨 **NOPE.** That’s a security risk.  
This lab shows the **proper** way:
- Create a secure IAM role
- Attach it to EC2
- Scope it to **least-privilege** access to S3
- All automated with Terraform

---

## ✅ Problem It Solves

| ❌ Before                     | ✅ After                                            |
|-----------------------------|----------------------------------------------------|
| Hardcoded AWS keys in EC2   | EC2 inherits temporary credentials via IAM Role   |
| Over-permissioned users     | Least-privilege access to a specific S3 bucket     |
| Manual configuration        | Automated using Terraform                          |
| Insecure S3 access          | Fine-grained IAM policy enforcement                |

---

## 🏗️ Lab Architecture

.
├── terraform/
│ ├── main.tf --> Sets up IAM Role, Instance Profile, EC2, S3
│ ├── iam.tf --> IAM Role & policy attachments
│ ├── variables.tf --> Input variables for flexibility
│ ├── outputs.tf --> Output EC2 IP, role name, etc.
│ └── providers.tf --> AWS provider config
├── diagrams/
│ └── iam-role-ec2-s3.drawio.png --> Visual of role delegation
├── scripts/
│ └── test-s3-access.sh --> Script to validate access from EC2
├── README.md
└── .gitignore

yaml
Copy
Edit

---

## 🖼️ Diagram – IAM Role Delegation

> EC2 → IAM Role → S3 Bucket  
> _No long-term credentials needed. This is best practice 101._

![IAM Role Diagram](https://raw.githubusercontent.com/Tommy813-lab/aws-iam-role-lab/main/diagrams/iam-role-ec2-s3.drawio.png)

---

## ⚙️ What It Does

Terraform will automatically deploy:

- 🔐 An IAM Role with scoped inline policy to S3
- 📦 An S3 Bucket for mock storage
- 💻 An EC2 Instance with the IAM Role via Instance Profile
- 🧪 A shell script to verify EC2-to-S3 access using role-based auth

---

## 🧪 Step-by-Step Lab Guide

### 1. Clone the Repo

```bash
git clone https://github.com/Tommy813-lab/aws-iam-role-lab.git
cd aws-iam-role-lab/terraform
2. Customize Variables
Create or edit terraform.tfvars:

hcl
Copy
Edit
region        = "us-east-1"
instance_type = "t2.micro"
bucket_name   = "charles-demo-bucket-1234"
3. Deploy the Lab
bash
Copy
Edit
terraform init
terraform apply
4. Connect to EC2 and Test S3 Access
bash
Copy
Edit
ssh -i my-key.pem ec2-user@<EC2_PUBLIC_IP>
bash test-s3-access.sh
You should see confirmation that the EC2 instance accessed the S3 bucket using its IAM role.

5. Clean Up Resources
bash
Copy
Edit
terraform destroy
🧠 Concepts You’ll Learn
Concept	Why It Matters
IAM Roles vs Users	Roles are temporary and safer
Least Privilege	Give access to only what’s necessary
Instance Profile	The glue between IAM Role and EC2
S3 Permissions	Control exactly what EC2 is allowed to do with S3

🚀 Real-World Use Cases
✅ EC2 apps needing secure S3 access
✅ Lambda roles with scoped permissions
✅ Cross-account IAM role delegation
✅ Avoiding long-term credential leaks in apps

🧠 Pro Tip from Charles
“If you're using aws configure on an EC2 instance, you're doing it wrong.
Let the IAM Role handle credentials like AWS intended.”

🗂️ Next Labs To Check Out
🔍 Proactive Monitoring with CloudWatch & SNS

📦 Secure Static Website with S3 + CloudFront

🧠 Cloud Infra Monitoring Lab

👨‍💻 Author
Charles Bucher
Cloud Support Engineer · AWS · Terraform · Real-World Problem Solver

GitHub;  @Tommy813-lab

LinkedIn:  Charles Bucher

Portfolio:  Charles-Portfolio/

