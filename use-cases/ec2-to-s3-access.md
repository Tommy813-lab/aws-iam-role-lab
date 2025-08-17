# EC2 to S3 Access Lab

## Scenario

You have an EC2 instance that needs to **read and write files to an S3 bucket**.  
**Problem:** Hardcoding AWS credentials on the EC2 instance is **insecure**.  

**Solution:** Use an **IAM Role attached to the EC2 instance** to grant scoped, temporary access to the S3 bucket.

---

## Step 1: Create an IAM Role

1. Log in to AWS and navigate to **IAM → Roles → Create Role**.  
2. Choose **AWS service → EC2** as the trusted entity.  
3. Attach a **policy that grants only necessary access** to the S3 bucket.  
   Example: `tommy813-ec2-s3-access-policy.json` (from your `policies` folder).  
4. Give the role a clear name, e.g.:  

