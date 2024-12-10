# AWS EFS Shared Storage Hands-On

This project demonstrates setting up **Amazon EFS** (Elastic File System) and connecting it to two EC2 instances with different operating systems (Ubuntu and Amazon Linux 2) to enable shared storage.

## **Objective**
- Create an EFS and connect it to multiple EC2 instances.
- Demonstrate shared storage capabilities across different OS environments.

## **Setup Steps**

### **1. Launch EC2 Instances**
- **Instance 1**: Ubuntu 22.04
- **Instance 2**: Amazon Linux 2
- Ensure both instances are in the same **VPC**.

### **2. Create EFS**
1. Navigate to the **Amazon EFS** service in the AWS Console.
2. Create a new EFS with:
   - **Default settings** for storage class and lifecycle policy.
   - **Mount targets** in the availability zones of the EC2 instances.
3. Attach a security group allowing **NFS traffic (port 2049)**.

### **3. Install Required Utilities**
- On **Ubuntu**:
  ```bash
  sudo apt update
  sudo apt install -y nfs-common
  
 # On Amazon Linux 2:
sudo yum install -y amazon-efs-utils

# mount the efs
Create a directory on both instances:
sudo mkdir /mnt/efs
Mount the EFS in to /mnt/efs
sudo mount -t nfs4 <file-system-id>.efs.<region>.amazonaws.com:/ /mnt/efs

 # Test the Shared Storage
Create a file in /mnt/efs on one instance:
echo "Hello from Ubuntu" | sudo tee /mnt/efs/test.txt

# Verify the file is accessible from the other instance:
cat /mnt/efs/test.txt
