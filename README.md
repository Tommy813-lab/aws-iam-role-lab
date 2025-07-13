🛡️ AWS IAM Role Lab
Securely delegate access across your AWS services like a pro




📚 Scenario:
“I have an EC2 instance that needs to talk to S3, but I don’t want to hardcode AWS credentials. What do I do?”

You use IAM Roles—that’s what.

This lab simulates a real-life support ticket scenario:

💬 “Hey Charles, the EC2 instance can't access the S3 bucket. Do I just paste in the access keys?”

🚨 NOPE. That’s a security risk. This lab shows you the proper way:
→ Create a secure IAM role, attach it to EC2, and scope it to least-privilege access to S3.

✅ Problem It Solves
❌ Before	✅ After
Hardcoded AWS keys in EC2	EC2 inherits temporary credentials from IAM Role
Over-permissioned users	Tight, scoped access only to S3 bucket
Manual configuration	Automated with Terraform
Insecure S3 access	Fine-grained policy enforcement

🏗️ Lab Architecture
pgsql
Copy
Edit
.
├── terraform/
│   ├── main.tf          --> Sets up IAM Role, Instance Profile, EC2, S3
│   ├── iam.tf           --> IAM Role & policy attachments
│   ├── variables.tf     --> Input variables for flexibility
│   ├── outputs.tf       --> Output the EC2 public IP, role name, etc
│   └── providers.tf     --> AWS provider config
├── diagrams/
│   └── iam-role-ec2-s3.drawio.png  --> Visual of role delegation
├── scripts/
│   └── test-s3-access.sh  --> Validates access from EC2 to S3
├── README.md
└── .gitignore
🖼️ Diagram – IAM Role Delegation


EC2 → IAM Role → S3 Bucket
No long-term credentials needed. This is best practice 101.

⚙️ What It Does
Terraform Deploys:
🔐 An IAM Role with a custom inline policy

🧾 An S3 Bucket for storing mock data

💻 An EC2 Instance with the role attached via Instance Profile

🧪 A shell script to test access from EC2 to S3

🧪 Step-by-Step Instructions
1. Clone the repo
bash
Copy
Edit
git clone https://github.com/Tommy813-lab/aws-iam-role-lab.git
cd aws-iam-role-lab/terraform
2. Customize variables
Edit terraform/variables.tf or create a terraform.tfvars:

hcl
Copy
Edit
region = "us-east-1"
instance_type = "t2.micro"
bucket_name = "charles-demo-bucket-1234"
3. Deploy infrastructure
bash
Copy
Edit
terraform init
terraform apply
4. Connect to EC2 and test S3 access
bash
Copy
Edit
ssh -i my-key.pem ec2-user@<EC2_PUBLIC_IP>
bash test-s3-access.sh
🧹 Clean Up
bash
Copy
Edit
terraform destroy
🧠 Concepts You’ll Learn
Concept	Why It Matters
IAM Roles vs Users	Roles are temporary and safer
Least Privilege	Only allow what’s needed—nothing more
Instance Profile	The glue between EC2 and IAM Role
S3 Permissions	Control exactly what your app can access

🚀 Real-World Use Cases
✅ Production EC2 apps needing secure S3 access
✅ Temporary Lambda roles with API access
✅ Cross-account access between AWS accounts
✅ Avoiding permanent credential leaks

🧠 Pro Tip from Charles
“If you're using aws configure on an EC2 instance, you're doing it wrong. Let the IAM Role handle it.”

🗂️ Next Labs To Check Out
🔍 Proactive Monitoring with CloudWatch & SNS

📦 Secure Static Website with S3 + CloudFront

🧠 Cloud Infra Monitoring Lab

👨‍💻 Author
Charles Bucher
Cloud Support Engineer · AWS · Terraform · Real-world Solutions
GitHub @Tommy813-lab | LinkedIn  https://www.linkedin.com/in/charles-bucher | Portfolio  https://tommy813-lab.github.io/Charles-Portfolio/
