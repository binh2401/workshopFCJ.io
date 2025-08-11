---
title : "Create SNS and IAM for Sending Email"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.2 </b> "
---

### 📬 Objective

In this step, we will:

- Create an **SNS Topic** to send an email when an order is placed successfully.
- Create an **IAM Policy** that allows the application to send notifications via SNS.
- Assign that permission to an EC2 Instance or backend service.

---

## 🛠️ Create an SNS Topic

1. Go to the [Amazon SNS](https://console.aws.amazon.com/sns/v3/home) service.
![Display Name](/images/2.prerequisite/image.png)

2. Select **Topics** from the left menu, then click **Create topic**.

![Display Name](/images/2.prerequisite/image2.png)

3. Choose **Standard** as the topic type.  
4. Enter a name for the topic, for example: `book-email`.  
![Display Name](/images/2.prerequisite/image3.png)

5. Keep the default settings and click **Create topic**.

---

## 📥 Subscribe an Email to Receive Notifications

1. After creating the topic, select it from the list.
2. In the **Subscriptions** tab, click **Create subscription**.

![Display Name](/images/2.prerequisite/image4.png)

3. Choose:
   - **Protocol**: `Email`
   - **Endpoint**: enter your email address to receive notifications (e.g., `user@example.com`)  
   ![Display Name](/images/2.prerequisite/Untitled.png)

4. Click **Create subscription**.

![Display Name](/images/2.prerequisite/image9.png)

> 📧 A confirmation email will be sent to the address you entered. **You must click the confirmation link** in that email to start receiving notifications.

![Display Name](/images/2.prerequisite/image10.png)

---

## 🔐 Create an IAM User to Send SNS Messages

In this section, you will create an **IAM User specifically for sending emails through Amazon SNS**. This user will have the `sns:Publish` permission to the topic you created.

---

### 1. Open the IAM Console

Go to the [IAM Management Console](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/home).

![IAM Console](/images/2.prerequisite/image5.png)

---

### 2. Create an IAM User

- Select **Users** → click **Create user**

---

### 3. Enter User Information

- Enter a user name, for example: `book-store-sns`
- Check **Programmatic access**

![Create User](/images/2.prerequisite/image6.png)

→ Click **Next**

---

### 4. Attach SNS Permissions

- Choose **Attach policies directly**
- Search for `AmazonSNSFullAccess` and check it (or attach a custom policy if you already created one)

![Set SNS Permissions](/images/2.prerequisite/image7.png)

Click **Next**

---

### 5. Review and Create IAM User

- Click **Create user**  
![Set SNS Permissions](/images/2.prerequisite/image8.png)

Create Access Key:

- Click **Create access key** (top right, under `Access key`)
- Follow the instructions to create an `Access key ID` and `Secret access key` pair

> ✅ **Note**: You can only view the `Secret access key` **once** at creation time. Save it securely for configuring in your application.

---

### 6. Use the Access Key in Your Application

You can use this Access Key to send emails via SNS using the appropriate SDK:

- For **ASP.NET MVC** (AWS SDK for .NET)
- Or **Python**, **Node.js**, **Java**, etc.

---

### 7. Configure AWS in `appsettings.json`

Add SNS configuration details to the `appsettings.json` file as follows:

```json
{
  "AWS": {
    "AccessKey": "Your AccessKey",
    "SecretKey": "Your SecretKey",
    "Region": "Your configured Region",
    "SnsTopicArn": "Your SnsTopicArn"
  }
}
```
{{% notice warning %}}
🔐 Security Warning: Do not commit your AccessKey and SecretKey to GitHub.
Instead, store them in environment variables or a .env configuration file.
{{% /notice %}}


