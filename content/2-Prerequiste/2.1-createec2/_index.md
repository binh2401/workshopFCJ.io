---
title : "Prepare VPC and EC2"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

In this step, we will create a VPC with 2 subnets: one public and one private.  
Then, we will create **1 Linux EC2 Instance** in the public subnet and **1 Windows EC2 Instance** in the private subnet.

The overall architecture after completing this step will look like this:

![VPC](/images/arc-01.png)

To learn how to create EC2 instances and a VPC with public/private subnets, you can refer to these lab guides:
  - [Introduction to Amazon EC2](https://000004.awsstudygroup.com/vi/)
  - [Working with Amazon VPC](https://000003.awsstudygroup.com/vi/) 


### Contents
  - [Create VPC](2.1.1-createvpc/)
  - [Create Public subnet](2.1.2-createpublicsubnet/)
  - [Create Private subnet](2.1.3-createprivatesubnet/)
  - [Create Security Group](2.1.4-createsecgroup/)
  - [Create Linux public server](2.1.5-createec2linux/)
  - [Create Windows private server](2.1.6-createec2windows/)
