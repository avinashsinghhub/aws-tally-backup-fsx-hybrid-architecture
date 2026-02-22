# Tally Backup & Hybrid File Server Architecture  
**AWS Region: AP-SOUTH-1**

---

## Overview

This repository documents a secure hybrid cloud architecture designed for:

- Encrypted offsite backup of Tally data
- Modernization of legacy NAS storage
- Secure hybrid connectivity between on-premises and AWS
- Automated monitoring and failure alerts
- Cost-optimized cloud storage

The production Tally workload remains on-premises on a Windows Server, while backups are stored securely in Amazon S3.  
Legacy NAS storage is replaced with Amazon FSx for Windows File Server.

---

## Architecture Objectives

- Protect business-critical Tally data from data loss
- Eliminate single-point-of-failure NAS dependency
- Implement encrypted cloud backups
- Provide scalable SMB file storage
- Maintain secure hybrid connectivity
- Enforce least-privilege access control
- Enable automated failure notifications

---

## High-Level Architecture
![Architecture](https://github.com/avinashsinghhub/aws-tally-backup-fsx-hybrid-architecture/blob/4ac6ebd9c51b2d160c727fba1d74fa2e85d7b30c/architecture/diagram.png)

### On-Premises Environment

- Windows Server hosting:
  - Tally Application
  - Tally Data (Local Disk)
- Duplicati (Encrypted Backup Agent)
- Site-to-Site IPSec VPN Gateway
- Office Users accessing Tally over LAN

### AWS Cloud (AP-SOUTH-1)

#### Backup Layer
- Amazon S3 (Intelligent-Tiering)
- IAM User (Scoped S3 Policy, Least Privilege)
- HTTPS Encrypted Upload from Duplicati

#### File Server Layer
- Amazon FSx for Windows File Server
- Accessed over SMB via IPSec VPN

#### Monitoring Layer
- Amazon SNS
- Email Notifications to Administrator
- Backup failure alerts

---

## Data Flow

1. Office users access Tally locally via LAN.
2. Tally data is stored on the Windows Server local disk.
3. Duplicati performs scheduled encrypted backups.
4. Backups are uploaded securely over HTTPS to Amazon S3.
5. S3 stores data using Intelligent-Tiering for cost optimization.
6. Backup failure events trigger Amazon SNS.
7. SNS sends alert emails to the administrator.
8. Office users access Amazon FSx via SMB over IPSec VPN.

---

## Security Controls

### Network Security
- Site-to-Site IPSec VPN
- No public endpoints exposed
- Private subnet deployment for FSx
- Restricted security group rules

### Data Protection
- HTTPS encryption for S3 uploads
- IPSec encryption for SMB traffic
- S3 encryption at rest
- FSx encryption at rest
- Encrypted backups via Duplicati

### Identity & Access Management
- Dedicated IAM user for backup
- Least-privilege S3 policy
- No console access for backup IAM user
- Scoped bucket-level permissions

---

## Storage Strategy

### Amazon S3
- Storage Class: Intelligent-Tiering
- Optimized for unpredictable access
- Scalable offsite backup storage

### Amazon FSx
- Replaces legacy NAS
- Managed Windows file server
- Native SMB support
- Scalable and highly available

---

## Backup Strategy

- Backup Frequency: Daily (configurable)
- Encryption: Enabled at source (Duplicati)
- Offsite Storage: Amazon S3
- Monitoring: SNS-based failure alerts
- Restore Testing: Quarterly recommended

---

## Business Impact

- Improved resilience against data loss
- Secure offsite encrypted backups
- Scalable cloud file storage
- Reduced operational overhead
- Eliminated NAS hardware dependency
- Hybrid model without production disruption

---

## Future Enhancements

- Cross-region S3 replication
- Backup lifecycle retention policies
- FSx automated backups
- Centralized logging and audit trail
- Disaster recovery runbook automation

---

## Author

Avinash Singh  
Cloud Architecture | AWS Infrastructure | Cost Optimization
