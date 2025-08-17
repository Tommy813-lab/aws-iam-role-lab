
---

## Step 2: Attach the Role to Your EC2 Instance

1. Go to **EC2 → Instances**.  
2. Select your instance and click **Actions → Security → Modify IAM Role**.  
3. Attach the role you just created (`EC2S3AccessRole`).  

> The instance now automatically inherits temporary credentials from this role.

---

## Step 3: Access S3 from EC2

1. SSH into your EC2 instance:

```bash
ssh -i my-key.pem ec2-user@<EC2_PUBLIC_IP>
