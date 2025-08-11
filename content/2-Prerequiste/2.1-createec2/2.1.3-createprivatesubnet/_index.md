---
title : "Create EC2 Security Group"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

## ℹ️ What is a Security Group?

A **Security Group** acts as a **virtual firewall**, controlling **inbound and outbound traffic** to AWS resources such as EC2.

- Each Security Group contains a set of **inbound rules** and **outbound rules**.
- It is applied to **each EC2 instance** or related services.

---

## 🛠️ Steps to Create a Security Group for EC2

### Step 1: Access AWS EC2 Console

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).  
2. In the service menu, select **EC2** under **Compute**.  
![VPC](/images/2.prerequisite/ec21.png)

---

### Step 2: Open Security Groups

- In the left navigation pane, under **Network & Security** → select **Security Groups**.  
![VPC](/images/2.prerequisite/ec22.png)  
- Click **Create Security Group**.

---

### Step 3: Enter basic information

- **Security group name**: A descriptive name for the Security Group.  
- **Description**: Details about the purpose of the Security Group.  
- **VPC**: Select the VPC where you want to apply it.  

![VPC](/images/2.prerequisite/ec22.png)

```txt
Example:
Name: web-server-sg
Description: Security group for application web server
VPC: vpc-0a1b2c3d
```

---

### 📥 Step 4: Configure Inbound Rules

Add rules to allow incoming traffic to your EC2 instance:

| **Traffic Type** | **Port** | **Description**                          |
|------------------|----------|------------------------------------------|
| HTTP             | 80       | Unsecured web access                     |
| HTTPS            | 443      | Secure web access                        |
| Custom TCP       | 5000     | Allow app running on port 5000           |
| SSH              | 22       | SSH access for server administration     |

> 🔒 **Security Note:**  
> In a production environment, **only allow SSH from trusted IP addresses**, e.g., `203.0.113.0/24`.  
> Avoid using `0.0.0.0/0` unless you are in a test environment or have other security layers in place.

---

### 📤 Step 5: (Optional) Configure Outbound Rules

- **Default:** Allow all outbound traffic.  
- You can restrict outbound traffic if tighter control is required in special environments.

---

![VPC](/images/2.prerequisite/ec23.png)

---

### Step 6: After completing the configuration, click **Create security group**.

![VPC](/images/2.prerequisite/ec24.png)

> 💡 **Pro Tip:**  
> You can **edit Security Group rules at any time**, and changes will be **applied immediately** to all resources associated with the Security Group.
