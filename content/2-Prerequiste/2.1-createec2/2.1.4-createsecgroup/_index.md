---
title : "Create Security Group for Amazon RDS"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

# Create Security Group for Amazon RDS

ℹ️ **Information:**  
A Security Group for Amazon RDS acts as a **virtual firewall** to control inbound and outbound network traffic to your database. Configuring the Security Group correctly is a crucial step to protect your data in AWS.

---

## 🛠️ Steps to Create a Security Group for RDS

### 1. Log in to AWS Management Console.

### 2. Access the **VPC** service
- Go to the Services menu.

- Select **VPC** under **Networking & Content Delivery**.
![VPC](/images/2.prerequisite/rdssc1.png)

### 3. Open the **Security Groups** list
- In the left navigation pane, under **Security**, choose **Security Groups**.
![VPC](/images/2.prerequisite/ec22.png)

### 4. Click the **Create security group** button to start the process.

---
![VPC](/images/2.prerequisite/rdssc2.png)

## 📝 Configure Basic Details

- **Security group name:** Enter a descriptive name for the Security Group.
- **Description:** Add a detailed description of the Security Group’s purpose.
- **VPC:** Select the VPC where you will deploy your RDS database.

---

## 🔐 Configure Inbound Rules

1. Select **MSSQL** from the **Type** list.
2. **Port 1433** will be auto-filled.
3. **Source:** Select **Anywhere-IPv4**.

> 🔒 **Security Note:**  
> Only allow connections from specific sources instead of opening the database port to all IP addresses (`0.0.0.0/0`). This follows the **principle of least privilege** and improves security.

---

## 📤 (Optional) Configure Outbound Rules

- By default, **all outbound traffic is allowed**.
- You can restrict it if you need higher security.

---

## ✅ Create Security Group

- Once you have completed the configuration, click **Create security group**.
- The new Security Group is now created and ready to be assigned to your **RDS DB instance**.

> ⚠️ **Warning:**  
> Do not use the **same Security Group** for both **EC2** and **RDS**.  
> Keeping Security Groups separate allows more precise access control and follows **security best practices**.

---

## 💡 Pro Tip

You can **edit Security Group rules at any time**, and changes will **apply immediately** to all resources associated with that Security Group.
