---
title : "Create a Connection to an EC2 Server"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

## Guide to Creating an Amazon EC2 Instance

ℹ️ **Information**: Amazon Elastic Compute Cloud (EC2) provides scalable computing capacity in the AWS cloud. Using EC2 allows you to deploy virtual servers without investing in physical hardware, helping you develop and deploy applications faster.

---

## 📌 Steps to Create an EC2 Instance

### 1. Access AWS Management Console
- Open your browser and go to the Amazon EC2 console:  
  👉 https://console.aws.amazon.com/ec2/
![EC2](/images/2.prerequisite/ec2sv1.png)
---

### 2. Launch an EC2 Instance
- On the EC2 console Dashboard, in the **Launch instance** box, select **Launch instance**.

![EC2](/images/2.prerequisite/ec2sv2.png)

---

## 1. Launch an Instance
![EC2](/images/2.prerequisite/ec2linux3.png)
### 🔖 Name and Tags
- **Instance name**: `book-store-server`

---

## 2. Application and OS Images (Amazon Machine Image)

### 🔹 Mode: `Quick Start`
- **Operating System**: Amazon Linux
- **Version**: `Amazon Linux 2023 AMI`
- **Details**:
  - Full name: `Amazon Linux 2023 AMI 2023.2.20240219.0 x86_64 HVM kernel-6.1`
  - Image ID: `ami-0c55b159cbfafe1f0`
  - Architecture: `x86_64`
  - Virtualization type: `HVM`
  - Root device type: `EBS`
  - Platform: `Linux`
  - **Free tier eligible** ✅

---

## 3. Instance Type

- **Instance type**: `t2.micro`
- 1 vCPU, 1 GiB RAM
- **Free tier eligible** ✅

---

## 4. Key Pair (Login)

- **Selected key pair**: `book-store`
- If you don’t have one yet, click **Create key pair**.

![EC2](/images/2.prerequisite/ec2linux1.png)
---

## 5. Network Settings

- **VPC**: `vpc-xxx (back-store-cloud-vpc)`
- **Subnet**: `subnet-xxx (back-store-cloud-public-sub-eastasia-b)`
- **Auto-assign public IP**: Enabled
- **Firewall (security group rules)**:
  - Mode: `Select existing security group`
  - **Security group**: `book-store-cloud-sg` (ID: `sg-034e625ff1fbdd04c`)
  - Open ports:
    - SSH (TCP port 22)
    - HTTP (TCP port 80)
    - HTTPS (TCP port 443)

---

## 6. Configure Storage

- **Default volume**:
  - Size: `10 GiB`
  - Type: `gp2 (General Purpose SSD)`
  - **Free tier eligible** ✅
- **Encrypted**: ❌ (Not encrypted)

---

## 7. Summary

- **Name**: `book-store-server`
- **AMI**: Amazon Linux 2023
- **Instance type**: `t2.micro`
- **Key pair**: `book-store`
- **Security group**: `book-store-cloud-sg`
- **Storage**: 10 GiB gp2
- **Free tier eligible**: ✅

---

## ✅ After Completing:

1. Click the **Launch instance** button.
![EC2](/images/2.prerequisite/ec2linux4.png)
2. Wait for the instance status to change from `pending` to `running`.
3. Connect to the instance via SSH using its public IP or DNS through MobaXterm or a terminal.

# Connect to an EC2 Instance via SSH using MobaXterm

ℹ️ **Information**:  
MobaXterm is an all-in-one application for Windows that provides various networking tools in a single interface, including:
- SSH client
- SFTP
- X11 server
- And more

---

## 🧰 Step 1: Download and Install MobaXterm

- Download MobaXterm from the official site: 👉 [MobaXterm Website](https://mobaxterm.mobatek.net/)
- Install the application following the instructions.

---

## 🔌 Step 2: Create a New SSH Session

1. Launch **MobaXterm**.
2. Click the **Session** icon in the top left corner.

---

## ⚙️ Step 3: Configure SSH Connection

In the configuration window:
- **Remote Host**: Enter the public IP or public DNS of your EC2 instance.
- **Port**: `22` (default SSH port)
- **User**: `ec2-user` (for Amazon Linux)

### ➕ Advanced SSH settings:
- Go to this tab to specify the path to the **private key file** (`.pem`) used for SSH connection.

🔒 **Security Note**:

- Ensure the `.pem` file has restricted permissions (readable only by the current user).
- On Linux/Mac, run: `chmod 400 file.pem`

---

## 🖥️ Step 4: Connect to the EC2 Instance

- Click **OK** to save and start the SSH session.
- If this is your first time connecting:
  - A warning about an **unknown host key** will appear.
  - Click **Yes** to continue.

---

## ✅ Verify Successful Connection

- Once connected, you will see the **terminal of the EC2 instance**.
- You can start running commands such as: `sudo yum update`, `top`, `htop`, ...
![EC2](/images/3.connect/ec2linuxconet1.png)

💡 **Tip**:
- MobaXterm automatically saves recent sessions.
- This allows you to easily reconnect without reconfiguring.

---

**🎉 Done!** You have successfully connected to your EC2 instance via SSH.
