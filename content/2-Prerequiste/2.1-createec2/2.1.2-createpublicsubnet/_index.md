---
title : "Create Public Subnet"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

## ℹ️ What is a DB Subnet Group?

A **DB Subnet Group** is a collection of subnets within a VPC designated for Amazon RDS databases.  
Creating a DB Subnet Group allows RDS to deploy database instances across **multiple Availability Zones (AZs)** to ensure:

- **High availability**
- **Fault tolerance**

---

## 🛠️ Steps to Create a DB Subnet Group

### Step 1: Access Amazon RDS

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).  
2. In the service menu, search for and select **Amazon RDS**.  
![VPC](/images/2.prerequisite/rds1.png)

### Step 2: Open the Subnet Groups interface

- In the left navigation pane → select **Subnet groups**.  

- Click the **Create DB Subnet Group** button.  
![VPC](/images/2.prerequisite/rds2.png)

---

### Step 3: Enter basic information

- **Name**: A descriptive name for the DB Subnet Group.  
- **Description**: A detailed description.  
- **VPC**: Select the VPC where you will deploy RDS.  

![VPC](/images/2.prerequisite/rds3.png)

```txt
Example:
Name: book-store-subnet-group
Description: book-store-subnet-group
VPC: vpc-0a1b2c3d
```

- Once done, click **Create**:  
![VPC](/images/2.prerequisite/rds4.png)
