# AWS NAT Gateway Project 🚀

This project demonstrates how to set up a **NAT Gateway** in AWS to allow private EC2 instances to access the internet securely while keeping them unreachable from the public internet.

---

## 📌 Architecture
            +-----------------------+
            |      Internet          |
            +-----------+------------+
                        |
                IGW (Internet Gateway)
                        |
    +-------------------+-------------------+
    |      Public Subnet (NAT Gateway)       |
    |  EC2 (Bastion / Testing Instance)      |
    +-------------------+-------------------+
                        |
               NAT Gateway (Elastic IP)
                        |
    +-------------------+-------------------+
    |      Private Subnet (No Public IP)     |
    |  EC2 Instance (Access Internet via NAT)|
    +-------------------+-------------------+
---

## 🛠 Steps to Build

### 1️⃣ Create a VPC
- CIDR: `10.0.0.0/16`

### 2️⃣ Create Subnets
- **Public Subnet**: `10.0.1.0/24`
- **Private Subnet**: `10.0.2.0/24`

### 3️⃣ Create and Attach Internet Gateway (IGW)
- Attach IGW to the VPC.
- Add route `0.0.0.0/0 → IGW` in **Public Route Table**.

### 4️⃣ Create NAT Gateway in Public Subnet
- Allocate Elastic IP for NAT Gateway.
- Add route `0.0.0.0/0 → NAT Gateway` in **Private Route Table**.

### 5️⃣ Launch EC2 Instances
- One in **Public Subnet** (for testing / bastion).
- One in **Private Subnet** (no public IP).

### 6️⃣ Security Groups
- Allow SSH (port 22) for Bastion Host.
- Allow outbound traffic for both instances.

---

## ✅ Testing NAT Gateway

On the **private EC2 instance**, run:
```bash
curl https://google.com
OR

bash
Copy code
sudo yum update -y
If you get output, the NAT Gateway is working fine. 🎉
-------------------------------------------------------------------
✍️ Author
Prajakta Pandaram
System Engineer | AWS & DevOps Enthusiast

