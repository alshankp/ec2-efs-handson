# AWS EFS Shared Storage Hands-On

This project demonstrates setting up **Amazon EFS** (Elastic File System) and connecting it to two EC2 instances with different operating systems (Ubuntu and Amazon Linux 2) to enable shared storage.

---

## **Features**

- Shared storage across multiple EC2 instances.
- Compatibility with different operating systems.
- Beginner-friendly step-by-step guide.

---

## **Table of Contents**

- [Objective](#objective)
- [Setup Steps](#setup-steps)
  - [1. Launch EC2 Instances](#1-launch-ec2-instances)
  - [2. Create EFS](#2-create-efs)
  - [3. Install Required Utilities](#3-install-required-utilities)
  - [4. Mount the EFS](#4-mount-the-efs)
  - [5. Test the Shared Storage](#5-test-the-shared-storage)
- [Enhancements](#enhancements)
- [License](#license)

---

## **Objective**

- Create an EFS and connect it to multiple EC2 instances.
- Demonstrate shared storage capabilities across different OS environments.

---

## **Setup Steps**

### **1. Launch EC2 Instances**

- **Instance 1**: Ubuntu 22.04
- **Instance 2**: Amazon Linux 2
- Ensure both instances are in the same **VPC**.

---

### **2. Create EFS**

1. Navigate to the **Amazon EFS** service in the AWS Console.
2. Create a new EFS with:
   - **Default settings** for storage class and lifecycle policy.
   - **Mount targets** in the availability zones of the EC2 instances.
3. Attach a security group allowing **NFS traffic (port 2049)**.

---

### **3. Install Required Utilities**

#### **On Ubuntu**:
```bash
sudo apt update
sudo apt install -y nfs-common
```

#### **On Amazon Linux 2**:
```bash
sudo yum install -y amazon-efs-utils
```

---

### **4. Mount the EFS**

1. Create a directory on both instances:
   ```bash
   sudo mkdir /mnt/efs
   ```
2. Mount the EFS to the directory:
   ```bash
   sudo mount -t nfs4 <file-system-id>.efs.<region>.amazonaws.com:/ /mnt/efs
   ```
   Replace `<file-system-id>` and `<region>` with your EFS details.

---

### **5. Test the Shared Storage**

1. Create a file in `/mnt/efs` on one instance:
   ```bash
   echo "Hello from Ubuntu" | sudo tee /mnt/efs/test.txt
   ```
2. Verify the file is accessible from the other instance:
   ```bash
   cat /mnt/efs/test.txt
   ```

---

## **Enhancements**

1. **Monitoring**: Use CloudWatch to monitor EFS performance and usage.
2. **Backup**: Enable automatic backups for EFS to ensure data safety.
3. **Access Points**: Configure EFS Access Points for specific user access.

---

## **License**

This project is licensed under the MIT License. Feel free to use and modify it for your own projects!

---

## **Feedback**

We love contributions and feedback! Feel free to open an issue or submit a pull request. If this project helped you, give it a ⭐️ and share it with others!
