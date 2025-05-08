# linux-no-space-journal-issue
Troubleshooting Ubuntu boot issue caused by “No space left on device” error preventing journal creation and password recovery.

# 🐧 Ubuntu Boot Issue: No Space Left on Device

This repository documents how to troubleshoot and solve an issue where an Ubuntu virtual machine (running on VMware) fails to boot due to the error: systemd-journald[xxxx]: Failed to create new system journal: No space left on device



# Ubuntu Boot Issue - No Space Left on Device

## 🧨 Problem

When booting into Ubuntu, system fails with the following error: systemd-journald[xxxx]: Failed to create new system journal: No space left on device



This issue is caused when the root filesystem becomes full, preventing the system from writing essential logs and continuing the boot process.

---

## ❗ The Problem

During boot, Ubuntu fails with repeated log messages from `systemd-journald`, stating it cannot create a new journal due to lack of space.

Typical symptoms include:
- Black screen with error logs
- Frozen boot process
- Cannot access graphical or text-based login

---

## ✅ Solution Guide

### 1. Boot into Recovery Mode

1. Restart your computer.
2. While booting, hold **Shift** (on BIOS) or press **Esc** (on UEFI) to bring up the GRUB menu.
3. Choose `Advanced options for Ubuntu`.
4. Select the entry with `(recovery mode)`.

---

### 2. Remount the Root Filesystem as Read/Write

Once you’re in the recovery shell (root shell prompt):

```bash
mount -o remount,rw /
```

3. Free Up Disk Space
Now that the filesystem is writable, clear space with the following steps:

Clean old logs:
```
journalctl --vacuum-time=1d
rm -rf /var/log/journal/*
```

```
rm -rf /var/tmp/*
rm -rf /tmp/*
```


Clear package cache:
```
apt clean
```



Find and remove large files:
```
du -ahx / | sort -rh | head -20

```



Then Restart your system to listen what I've done

```
reboot
```

