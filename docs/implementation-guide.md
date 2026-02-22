# Implementation Guide

## 1. On-Premises Setup

### 1.1 Windows Server

- Install Tally application.
- Store Tally data on local disk.
- Configure proper NTFS permissions.
- Ensure server time synchronization.

### 1.2 Install Duplicati

- Install Duplicati on the Windows Server.
- Configure encryption with a strong passphrase.
- Store passphrase securely offline.

---

## 2. AWS Setup

### 2.1 Create S3 Bucket

- Region: ap-south-1
- Enable Block Public Access (all options ON)
- Enable default encryption (SSE-S3 or SSE-KMS)
- Configure Intelligent-Tiering
- Do not allow public access

### 2.2 Create IAM User

- Programmatic access only
- No console login
- Attach custom S3 least-privilege policy
- Restrict access to specific bucket and prefix
- Store access keys securely

Required permissions:

- s3:PutObject
- s3:GetObject
- s3:DeleteObject
- s3:ListBucket (restricted to prefix)

### 2.3 Configure Duplicati Destination

- Storage Type: Amazon S3
- Region: ap-south-1
- Use SSL: Enabled
- Storage Class: Intelligent-Tiering
- Bucket name: your-bucket-name
- Folder path: dedicated prefix
- Test connection before saving

---

## 3. Configure VPN Connectivity

- Establish Site-to-Site IPSec VPN.
- Configure routing between office network and AWS VPC.
- Restrict FSx access to office IP range.
- Validate SMB connectivity from on-premises to FSx.

---

## 4. Configure Amazon FSx

- Deploy FSx for Windows in private subnet.
- Join to domain if required.
- Configure SMB shares.
- Apply NTFS permissions.
- Restrict access via security groups.

---

## 5. Configure Monitoring

- Create SNS Topic.
- Subscribe administrator email.
- Configure S3 event or monitoring mechanism.
- Test failure notification.

---

## 6. Backup Schedule

- Frequency: Daily
- Time: Off-business hours
- Retention: Defined by business policy
- Quarterly restore test recommended
