---
title : "Overview and Configuration of AWS WAF and CloudFront"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

# 🔐 I. AWS WAF Overview

**AWS WAF (Web Application Firewall)** is a web application firewall service that helps protect websites or APIs from common threats such as:

- SQL Injection  
- Cross-Site Scripting (XSS)  
- DDoS attacks (when combined with **AWS Shield**)  
- Unusual requests (based on IP, country, header, etc.)

---

## 🛠️ II. Steps to Configure AWS WAF

#### 1. Create an Application Load Balancer (ALB)
- Go to **EC2 Console** → **Load Balancers** → **Create Load Balancer**  
![FWD](/images/5.fwd/waf3.png)
- Select type: **Application Load Balancer**
- Configuration:
  - Set ALB name
  - Select schema: Internet-facing (if the website is public)
  - Select VPC, Subnet
  - Configure security group to open ports 80/443  
![FWD](/images/5.fwd/waf4.png)

#### 2. Create a Target Group
- During ALB creation, select **Create a new target group**  
![FWD](/images/5.fwd/waf8.png)
- Target type: **Instance**
- Select protocol: **HTTP or HTTPS**
- Add **EC2 instances** running your website to the target group  
![FWD](/images/5.fwd/waf5.png)  
![FWD](/images/5.fwd/waf6.png)  
![FWD](/images/5.fwd/waf7.png)  

![FWD](/images/5.fwd/waf9.png)  
![FWD](/images/5.fwd/waf10.png)  
![FWD](/images/5.fwd/waf11.png)  

#### 3. Attach AWS WAF to the ALB
- Go to **AWS WAF & Shield**
- Select **Web ACLs** → **Create Web ACL**
- In the **Association** step, choose the ALB you created

---

### 1. Create a Web ACL (Access Control List)
- Go to **AWS Console** → Search for **WAF & Shield**  
![FWD](/images/5.fwd/image.png)
- Select **Web ACLs** → **Create web ACL**  
![FWD](/images/5.fwd/waf1.png)
- Name it, select **Region** if using **ALB**, or **CloudFront** if using CDN.  
![FWD](/images/5.fwd/waf2.png)

![FWD](/images/5.fwd/waf12.png)  

### 2. Choose the Resource to Protect
- Attach the Web ACL to one of the following:
  - **Application Load Balancer (ALB)**
  - **Amazon API Gateway**
  - **Amazon CloudFront** (recommended for global websites)

### 3. Add Rules to the Web ACL
You can choose:

#### ✅ AWS Managed Rule Groups:
![FWD](/images/5.fwd/waf13.png)  
![FWD](/images/5.fwd/waf14.png)  

### 4. Configure Action for Each Rule
- `Allow`: Permit
- `Block`: Deny
- `Count`: Log only (good for testing before enforcement)

### 5. Associate Web ACL with the Resource
Once created, attach the Web ACL to the resource you want to protect:

Client → CloudFront (with AWS WAF) → ALB → EC2/Laragon (.NET App)  
![FWD](/images/5.fwd/waf15.png)  
![FWD](/images/5.fwd/waf16.png)  

---

# Integrating AWS CloudWatch into an ASP.NET MVC Application

## ✅ Objective
- Log errors and system logs from **ASP.NET MVC** to **AWS CloudWatch Logs**
- Automatically create Log Group/Stream if not already existing
- No need to install the CloudWatch Agent

---

## 🧰 Requirements
- ASP.NET MVC application (Core or .NET Framework)
- AWS account and IAM user with permissions to write to CloudWatch Logs

---

## 🔧 Step 1: Install AWS Logger Package

Open terminal or Package Manager Console and run:

```bash
dotnet add package AWS.Logger.AspNetCore
```

> If you are using older .NET Framework MVC, use:  
> `AWS.Logger.Log4Net` or `AWS.Logger.NLog` depending on your logging framework.

---

## ⚙️ Step 2: Configure `appsettings.json`

```json
{
  "AWS": {
    "Region": "ap-southeast-1",
    "LogGroup": "MvcAppLogGroup"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning"
    }
  }
}
```

---

## 🧬 Step 3: Configure Logger in Code

### ✅ For ASP.NET Core MVC (.NET 6 and above):

Edit `Program.cs`:

```csharp
using AWS.Logger.AspNetCore;

var builder = WebApplication.CreateBuilder(args);

builder.Logging.AddAWSProvider(builder.Configuration.GetAWSLoggingConfigSection());

builder.Services.AddControllersWithViews();
var app = builder.Build();

app.UseRouting();
app.UseAuthorization();
app.MapDefaultControllerRoute();
app.Run();
```

---

## 🔐 Step 4: Configure AWS Access Permissions

### 👉 If running on EC2:
Assign an IAM Role to the EC2 instance with permissions:

```json
{
  "Effect": "Allow",
  "Action": [
    "logs:CreateLogGroup",
    "logs:CreateLogStream",
    "logs:PutLogEvents"
  ],
  "Resource": "*"
}
```

### 👉 If running locally (dev):
Create `~/.aws/credentials` on Linux/Mac or `C:\Users\<username>\.aws\credentials` on Windows:

```ini
[default]
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
```

---

## 🧪 Step 5: Add Logging in Controller

```csharp
private readonly ILogger<HomeController> _logger;

public HomeController(ILogger<HomeController> logger)
{
    _logger = logger;
}

public IActionResult Index()
{
    _logger.LogInformation("Homepage accessed at " + DateTime.Now);
    return View();
}
```

---

## 📊 Step 6: Check Logs in AWS

1. Go to **AWS Console > CloudWatch > Log groups**
2. Select `MvcAppLogGroup`
3. Choose the log stream to view details

---

## 🧩 Additional Notes
- You can use **AWS X-Ray** to trace performance if the application is complex.
- You can also integrate `LogLevel`, `EventID`, and `Exception` for more detailed logs.

---

**Good luck with your implementation!**
