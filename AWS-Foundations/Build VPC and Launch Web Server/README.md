# Lab 2: Build your VPC and Launch a Web Server

## Lab Overview and Objectives

In this lab, you will:

1. Create a VPC.
2. Create subnets.
3. Configure a security group.
4. Launch an EC2 instance into a VPC.

---

## Scenario

![Scenario](images/Scenario.png)

---

## Task 1: Create Your VPC

### Steps

1. From **Services**, search for and choose **VPC** to open the VPC console.
2. Choose **Create VPC**.

![VPC-dashboard](images/create-vpc.png)

3. **VPC Configuration:**

![VPC Config](images/1.png)
![VPC Config](images/2.png)
![VPC Config](images/3.png)
![VPC Config](images/4.png)
![VPC Config](images/5.png)

### VPC Review
![VPC Review](images/review.png)

![VPC Review](images/r2.png)

4. Click **Create VPC**.

> **Note:** The NAT Gateway will take a few minutes to activate.

![VPC Created](images/view1.png)

---

## Task 2: Create Additional Subnets

### Steps

1. In the left navigation pane, choose **Subnets**.
2. Choose **Create subnet** then configure:

![Create Subnet](images/create-subnet.png)
![Subnet Config](images/C2.png)
![Subnet Config](images/C3.png)

**The Public Subnet has been created successfully:**

![Public Subnet](images/public-subnet.png)

3. Choose **Create subnet** again.

> **Note:** The second public subnet was created. You will now create a second private subnet.

4. Choose **Create subnet** then configure:

![Private Subnet Config](images/private-subnet.png)
![Private Subnet Config](images/P2.png)
![Private Subnet Config](images/P3.png)

5. Choose **Create subnet**.

**The Private Subnet has been created successfully:**

![Private Subnet Created](images/createing-private.png)

---

### Route Tables Configuration

6. In the left navigation pane, choose **Route tables**.
7. Select the **lab-rtb-private1-us-east-1a** route table.

![Route Table](images/Route.png)

8. In the lower pane, choose the **Routes** tab.
9. Choose the **Subnet associations** tab.
10. In the **Explicit subnet associations** panel, choose **Edit subnet associations**.
11. Leave **lab-subnet-private1-us-east-1a** selected and also select **lab-subnet-private2**.
12. Choose **Save associations**.

![Edit Subnet Associations](images/change.png)

13. In the lower pane, choose the **Subnet associations** tab again.
14. In the **Explicit subnet associations** panel, choose **Edit subnet associations**.
15. Leave **lab-subnet-public1-us-east-1a** selected and also select **lab-subnet-public2**.

![Edit Public Subnets](images/edit-public.png)
![View Public Subnets](images/view2.png)

---

## Task 3: Create a VPC Security Group

1. In the left navigation pane, choose **Security groups**.

![Create Security Group](images/create-securitygroup.png)

2. Choose **Create security group** and configure:

![Security Group Configuration](<images/security group.png>)

3. Scroll to the bottom of the page and choose **Create security group**.

---

## Task 4: Launch a Web Server Instance

1. From **Services**, search for and choose **EC2**.
2. From the **Launch instance** menu, choose **Launch instance**.
3. Configuration:

![Launch Instance](images/launche1.png)
![Launch Instance](images/L2.png)
![Launch Instance](images/L3.png)
![Launch Instance](images/L4.png)
![Launch Instance](images/L5.png)

**The instance launched successfully:**

![Instance Launched](images/launched.png)

4. Choose **View all instances**.
5. Wait until **Web Server 1** shows **2/2 checks passed**, then select it.

![Web Server](images/web-server.png)

6. Copy the **Public IPv4 DNS** value from the **Details** tab:

```
http://ec2-54-166-135-53.compute-1.amazonaws.com/
```

---

## Final Work

![Final Work](images/Final-Work.png)
