# Lab 3: Introduction to Amazon EC2

## Lab overview

![Overview](images/overview.png)

---

## Lab objectives

- Launch a web server with termination protection enabled  
- Monitor Your EC2 instance  
- Modify the security group that your web server is using to allow HTTP access  
- Resize your Amazon EC2 instance to scale and enable stop protection  
- Explore EC2 limits  
- Test stop protection  
- Stop your EC2 instance  

---

## Task 1: Launch Your Amazon EC2 Instance

### Steps

1. In the AWS Management Console choose **Services**, choose **Compute** and then choose **EC2**.  

![Compute Ec2](images/compute.png)

2. Choose the **Launch instance** menu and select **Launch instance**.

---

### Step 1: Name and tags

1. Name the instance **Web Server**.

![Server Name](images/servername.png)

---

### Step 2: Application and OS Images (Amazon Machine Image)

1. In the list of available Quick Start AMIs, keep the default **Amazon Linux AMI** selected.  
2. Also keep the default **Amazon Linux 2023 AMI** selected.

![Os Image](images/Osimage.png)

---

### Step 3: Instance type

1. Keep the default **t2.micro** selected.

![Instance Type](images/instance-type.png)

---

### Step 4: Key pair (login)

1. For **Key pair name - required**, choose **vockey**.

![Key Pair](images/Key-pair.png)

---

### Step 5: Network settings

1. Choose **Edit**.  
2. For **VPC**, select **Lab VPC** and keep the subnet as default **public subnet1**.

![VPC](images/Network-setting.png)

3. Under **Firewall (security groups)**, choose **Create security group** and configure:

Security group name: Web Server security group  
Description: Security group for my web server  

4. Under **Inbound security group rules**, notice that one rule exists. Remove this rule.

![Firewall](images/Firewall.png)

---

### Step 6: Configure storage

1. In the **Configure storage** section, keep the default settings.

![Storage](images/Storage.png)

---

### Step 7: Advanced details

1. Expand **Advanced details**.  
2. For **Termination protection**, select **Enable**.

![Advanced details](images/Advanced1.png)

3. Scroll to the bottom of the page and copy and paste the code shown below into the **User data** box:

```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

![User Data](images/advanced2.png)

---

### Step 8: Launch the instance

1. At the bottom of the **Summary panel**, choose **Launch instance**.  
   You will see a Success message.

![Instance Launched](images/launch-instance.png)

2. Choose **View all instances**.  
3. In the Instances list, select **Web Server**.  
4. Review the information displayed in the **Details** tab.  
   The instance is assigned a Public IPv4 DNS that you can use to contact the instance from the Internet.  
5. Wait for your instance to display:

Instance State: Running  
Status Checks: 2/2 checks passed  

![Web Server Instance](images/Web-Server.png)

---

## Task 2: Monitor Your Instance

### Steps

1. Choose the **Status checks** tab.  
   Notice that both the System reachability and Instance reachability checks have passed.

![Reachability passed](images/reachability.png)

2. Choose the **Monitoring** tab.

![Monitoring](images/Monitoring.png)

3. In the **Actions** menu, select **Monitor and troubleshoot → Get system log**.

![Troubleshoot and Logs](images/Logs.png)

4. Scroll through the output and note that the HTTP package was installed from the user data.

![System Logs](images/system-logs.png)

5. Choose **Cancel**.  
6. Ensure Web Server is still selected. Then, from **Actions**, select  
   **Monitor and troubleshoot → Get instance screenshot**.

![Instance Troubleshoot and Screenshot](images/screenshoot.png)

This shows what your Amazon EC2 instance console would look like if a screen were attached.

![Instance Screenshot](images/instance-screenshot.png)

7. Choose **Cancel**.

---

## Task 3: Update Your Security Group and Access the Web Server

### Steps

1. Ensure Web Server is still selected. Choose the **Details** tab.  
2. Copy the Public IPv4 address of your instance.  
   Example: 54.226.100.67  
3. Open a new browser tab, paste the IP address, and press Enter.

**Question:** Are you able to access your web server? Why not?  

You are not currently able to access your web server because the security group is not permitting inbound traffic on port 80 (HTTP).

4. Return to the EC2 Console tab.  
5. In the left navigation pane, choose **Security Groups → Inbound rules**.  
   The security group currently has no inbound rules.

![Inbound Role](images/inpound-role.png)

6. Choose **Edit inbound rules → Add rule** and configure:

Type: HTTP  
Source: Anywhere-IPv4  

Choose **Save rules**.

![Edit Rules](images/edit-rules.png)

7. Return to the web server tab and refresh the page.  
   You should see: **Hello From Your Web Server!**

![Hello Server](images/Hello-Server.png)

---

## Task 4: Resize Your Instance: Instance Type and EBS Volume

### Step 1: Stop Your Instance

- Choose **Instances**  
- Select **Web Server**  
- From **Instance state**, select **Stop instance**  
- Choose **Stop**

![Stop instance](images/stop-instance.png)

Wait until the Instance state displays: **Stopped**

![Stopped Instance](images/stopped.png)

---

### Step 2: Change The Instance Type and Enable Stop Protection

- Select Web Server  
- From **Actions → Instance settings → Change instance type**

Instance Type: t2.small  

Choose **Apply**

![Change Instance Type](images/change-type.png)

- From **Actions → Instance settings → Change stop protection**  
- Select **Enable** and save

![Change Stop Protection](images/Stop-protection.png)

---

### Step 3: Resize the EBS Volume

- Choose the **Storage** tab  
- Select the **Volume ID**

![Modify Volume](images/modify-volum.png)

- Change the size to: 10  
- Choose **Modify** and confirm

![Modify](images/Modify.png)

---

### Step 4: Start the Resized Instance

- Choose **Instances**  
- Select Web Server  
- From **Instance state**, select **Start instance**

![Start Instance](images/start-instance.png)

---

## Task 5: Explore EC2 Limits

### Steps

1. Search for **Service Quotas**.  
2. Choose **AWS services → Amazon EC2**.

![AWS Services](images/AWS-services.png)

3. In the Find quotas search bar, search for **running on-demand** and observe the filtered list.

![Services Quotas](images/services-quotas.png)

---

## Task 6: Test Stop Protection

### Steps

1. Return to **EC2 → Instances**.  
2. Select Web Server and try to stop it.

![Stop Instance](images/stop-again.png)

A message appears indicating stop protection is enabled.

![Failed To Stop](images/failed-stop.png)

3. From **Actions → Instance settings → Change stop protection**  
   Remove the check next to Enable and save.

![Change Stop Protection](images/Change-stop.png)

4. Select Web Server again and stop the instance.

![Stop Instance](images/Can-stop.png)

---

## Final Work

![Final Work](images/Final.png)

---

## Additional Resources

Launch Your Instance  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/LaunchingAndUsingInstances.html  

Amazon EC2 Instance Types  
https://aws.amazon.com/ec2/instance-types  

Amazon Machine Images (AMI)  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html  

Amazon EC2 - User Data and Shell Scripts  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html  

Amazon EC2 Root Device Volume  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/RootDeviceStorage.html  

Security Groups  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html  

Amazon EC2 Service Limits  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html  

Termination Protection for an Instance  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html  
