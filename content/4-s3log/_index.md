---
title : "Create RDS Database and Deploy Website"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

# 1. Install Git on Amazon EC2 (Amazon Linux 2023)

### Step 1: Update the system

```bash
sudo dnf update -y
sudo dnf search git
sudo dnf install git -y
git --version
```
![EC2](/images/4.s3/git.png)

### Step 2: Install ASP.NET on Amazon EC2 Linux 2023 and clone files from Git

```bash
# Install .NET SDK & Runtime
sudo dnf install -y dotnet-sdk-8.0
sudo dnf install -y aspnetcore-runtime-8.0
# Check version
dotnet --version
```
+ After verifying the version, clone the repository:

```bash
git clone https://github.com/binh2401/FCJ.git
```

![EC2](/images/4.s3/moba1.png)

---

# Guide to Creating an RDS SQL Server on AWS

Amazon RDS supports deploying **Microsoft SQL Server** as a managed service.  
This guide will help you set up a SQL Server instance quickly and securely.

## 🔧 Steps

### Step 1: Open Amazon RDS Console

- Go to: [https://console.aws.amazon.com/rds/](https://console.aws.amazon.com/rds/)
- In the left navigation panel → choose **Databases**  
![EC2](/images/4.s3/rdscr3.png)

- Click **Create database**

---

### Step 2: Choose creation method

- Select **Standard create** (to fully customize the setup)
- Engine: choose **Microsoft SQL Server**

---

### Step 3: Choose version and edition

- **Edition**:
  - SQL Server Web Edition
  - SQL Server Express Edition
  - SQL Server Standard Edition
  - SQL Server Enterprise Edition (for advanced features)
