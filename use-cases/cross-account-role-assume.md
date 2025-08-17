
# Cross-Account Role Assume

## Scenario

You manage multiple AWS accounts: a **development account** and a **production account**.  
You need a **secure way** for resources or users in the development account to access resources in the production account **without sharing long-term credentials**.

---

## Solution: IAM Role Assumption

AWS allows you to create a **role in the target account** (production) that can be assumed by a **trusted principal** in another account (development).

---

## Step 1: Create Role in Production Account

1. Sign in to the **production AWS account**.  
2. Navigate to **IAM → Roles → Create Role**.  
3. Choose **Another AWS account** as trusted entity.  
4. Enter the **Account ID** of the development account.  
5. Attach a policy granting the required permissions (e.g., `S3ReadOnlyAccess`, `DynamoDBReadOnlyAccess`).  
6. Give the role a descriptive name:  
