
# Security Design

## Network Security

- Site-to-Site IPSec VPN encryption
- No public endpoints
- Private subnet deployment for FSx
- Restricted security group rules

## Data Encryption

- HTTPS encryption for S3 uploads
- IPSec encryption for SMB traffic
- S3 encryption at rest (SSE-S3 or SSE-KMS)
- FSx encryption at rest

## Identity and Access Management

- Dedicated IAM user for Duplicati
- Least-privilege S3 policy
- No administrative permissions granted
- No console access for backup user
- Secure storage of access keys

## Monitoring and Alerts

- SNS topic for backup failure notifications
- Email-based alerting
- Periodic review of IAM permissions

## Risk Mitigation

- Offsite encrypted backup
- Removal of single NAS dependency
- Scalable storage model
- Controlled hybrid connectivity
