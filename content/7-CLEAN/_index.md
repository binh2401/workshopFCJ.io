---
title: "Cleanup"
date: 2025-08-05
weight: 7
chapter: false
pre: "<b> 7. </b>"
---

## 🧨 Notes before deleting

- Always double-check if the resource is currently in use.
- Backup important data (if needed) before deleting.

---

## 🧹 1. Delete VPC manually

### Step 1: Open VPC Dashboard  
- Go to: [https://console.aws.amazon.com/vpc](https://console.aws.amazon.com/vpc)  
- Navigate to **Your VPCs**

### Step 2: Delete resources inside the VPC:
- Subnets
- Route tables
- Internet gateways
- NAT gateways
- Security groups (custom ones)

### Step 3: Delete VPC
- Select the VPC → **Actions** → **Delete VPC**

> ⚠️ You cannot delete a VPC if it still contains resources.

---

## 💾 2. Delete RDS Instance manually

### Step 1: Open RDS Dashboard  
- Go to: [https://console.aws.amazon.com/rds](https://console.aws.amazon.com/rds)

### Step 2: Go to **Databases**
- Select the DB to delete → **Actions > Delete**

### Step 3: Choose whether to keep the final snapshot
- Check `Skip final snapshot` if you do not need to keep it

---

## 🔐 3. Delete Security Group

- Go to: **EC2 Dashboard** → **Security Groups**
- Select the group → **Actions > Delete**

> Security groups can only be deleted if they are not attached to any EC2 instance or resource.

---

## 📊 4. Delete Log Group in CloudWatch

- Go to: [https://console.aws.amazon.com/cloudwatch](https://console.aws.amazon.com/cloudwatch)
- Select **Log groups** → check the log group → **Actions > Delete log group**

---

## 🔥 5. Delete WAF Web ACL

- Go to: [https://console.aws.amazon.com/wafv2](https://console.aws.amazon.com/wafv2)
- Select the Web ACL
- Click **Delete**

> If attached to ALB or CloudFront, detach it first.

---

## 📁 6. Delete S3 Bucket

- Go to: [https://s3.console.aws.amazon.com/s3](https://s3.console.aws.amazon.com/s3)
- Click the bucket → **Empty** to delete all files
- Then **Delete bucket**

---

## 🧬 7. Delete Neptune Cluster

### Step 1: Open Neptune Dashboard
- Go to: [https://console.aws.amazon.com/neptune](https://console.aws.amazon.com/neptune)

### Step 2: Delete all instances
- Select each **DB instance** in the cluster
- Click **Actions > Delete**

### Step 3: Delete the cluster
- Once all instances are removed, select the **Cluster**
- Click **Delete cluster**
- Choose whether to **Skip final snapshot** (only skip if data is no longer needed)

> ⚠️ You must remove associated parameter groups and subnet groups if you no longer need them.

---

## ✅ Summary

- Always confirm before deleting.
- Use tagging to quickly identify unused resources.
- Set up billing alerts to avoid costs from forgotten resources.
