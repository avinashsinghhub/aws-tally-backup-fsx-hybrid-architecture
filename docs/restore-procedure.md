# Restore Procedure

## 1. Restore from S3 Backup

### Step 1: Identify Backup Version
- Access Duplicati interface.
- Select required backup date.

### Step 2: Authenticate
- Enter encryption passphrase.

### Step 3: Select Files
- Choose required Tally data folders.
- Confirm restore location.

### Step 4: Restore
- Restore to original or alternate path.
- Validate file integrity.
- Restart Tally services if required.

---

## 2. Full Server Failure Scenario

1. Provision replacement Windows Server.
2. Install Tally.
3. Install Duplicati.
4. Configure S3 IAM credentials.
5. Restore latest backup.
6. Validate Tally functionality.

---

## 3. FSx File Restore

If shared files are lost:

1. Access FSx share.
2. Restore from available backup/versioning.
3. Verify NTFS permissions.
4. Notify users after validation.

---

## 4. Restore Testing

- Perform quarterly restore drill.
- Validate recovery time.
- Confirm encryption passphrase availability.
- Document results.
