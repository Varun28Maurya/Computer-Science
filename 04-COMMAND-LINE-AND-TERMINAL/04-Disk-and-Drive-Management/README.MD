
# Lesson 04: Disk and Drive Management in Windows CMD

> **Module:** Command Line and Terminal  
> **Topic:** Windows Command Prompt (CMD)  
> **Lesson:** 04 — Disk and Drive Management  
> **Level:** Beginner to Advanced

---

# 1. Introduction

Disk and drive management involves working with storage devices, partitions, volumes, and file systems.

Windows CMD provides several commands to inspect and manage storage.

Using these commands, you can:

- Identify available drives.
- Display volume information.
- View disk labels and serial numbers.
- Check file system errors.
- Display free disk space.
- Manage volume labels.
- Inspect partitions.
- Manage disks using DiskPart.
- Check and repair certain file system problems.

## 1.1 Important Storage Terminology

| Term | Meaning |
|---|---|
| Physical Disk | Actual storage device, such as an HDD or SSD |
| Partition | A logical division of a physical disk |
| Volume | A formatted storage area that Windows can access |
| Drive Letter | A letter assigned to a volume, such as C: or D: |
| File System | Structure used to organize and store files |
| NTFS | Common Windows file system |
| FAT32 | Older file system with broad compatibility |
| exFAT | File system commonly used for removable storage |
| Sector | Smallest addressable unit of physical storage |
| Cluster | Allocation unit used by a file system |

## 1.2 Understanding the Storage Structure

A simplified storage structure:

```text
Physical Disk
    |
    +--- Partition 1
    |       |
    |       +--- Volume C:
    |               |
    |               +--- Windows
    |               +--- Program Files
    |               +--- Users
    |
    +--- Partition 2
            |
            +--- Volume D:
                    |
                    +--- Documents
                    +--- Projects
                    +--- Backups
```

A partition and a volume are related but not identical concepts. A volume is the storage area exposed to Windows as a usable file system.

---

# 2. Displaying Available Drives

## 2.1 Switching Drives

To switch to drive D:

```cmd
D:
```

To switch to drive E:

```cmd
E:
```

To switch back to drive C:

```cmd
C:
```

## 2.2 Display Current Drive and Directory

```cmd
cd
```

This displays the current working directory.

Example:

```text
C:\Users\Varun\Documents
```

## 2.3 Display All Available Drive Information

```cmd
wmic logicaldisk get name
```

**Note:** WMIC is deprecated in modern Windows versions and may not be installed or available. Use PowerShell or other supported Windows tools when WMIC is unavailable.

An alternative is:

```cmd
fsutil fsinfo drives
```

This displays available drive letters.

Some `fsutil` operations require Administrator privileges.

---

# 3. VOL — Display Volume Information

The `vol` command displays the volume label and serial number of a disk.

Syntax:

```cmd
vol [drive:]
```

Example:

```cmd
vol C:
```

Possible output:

```text
Volume in drive C is Windows
Volume Serial Number is XXXX-XXXX
```

Display information for drive D:

```cmd
vol D:
```

### Important Points

- The volume label is the name assigned to a volume.
- The volume serial number is assigned when the volume is formatted.
- The serial number displayed by `vol` is not the same as the physical disk's manufacturer serial number.

---

# 4. LABEL — Manage Volume Labels

The `label` command displays or changes the volume label.

Syntax:

```cmd
label [drive:] [label]
```

Display the current label:

```cmd
label C:
```

Change the volume label:

```cmd
label D: Backup
```

Remove the volume label by providing an empty label when prompted.

### Important Points

- Changing a volume label does not format the disk.
- A volume label is simply a name used to identify a volume.
- Do not confuse changing a label with changing a drive letter.

---

# 5. FSUTIL — File System Utilities

`fsutil` is a command-line utility used to perform advanced file system operations.

Syntax:

```cmd
fsutil [command]
```

It contains several subcommands.

## 5.1 Display Available Drives

```cmd
fsutil fsinfo drives
```

## 5.2 Display File System Information

```cmd
fsutil fsinfo volumeinfo C:
```

This displays information about the specified volume.

## 5.3 Display NTFS Information

```cmd
fsutil fsinfo ntfsinfo C:
```

This displays NTFS-related volume information.

## 5.4 Display Volume Statistics

```cmd
fsutil volume diskfree C:
```

This displays information about available and total disk space.

### Important Points

- Some `fsutil` commands require Administrator privileges.
- The available subcommands depend on Windows version and file system.
- `fsutil` is an advanced administrative utility.
- Do not modify file system settings without understanding their impact.

---

# 6. CHKDSK — Check Disk

`chkdsk` checks a volume's file system and reports its status.

It can also attempt repairs when suitable options are provided.

Syntax:

```cmd
chkdsk [drive:] [options]
```

## 6.1 Basic Disk Check

```cmd
chkdsk C:
```

This checks the specified volume and displays a report.

## 6.2 Fix Logical File System Errors

```cmd
chkdsk C: /f
```

The `/f` option fixes file system errors.

Windows may require exclusive access to the volume. If the volume is in use, you may be asked whether to schedule the check for the next restart.

## 6.3 Locate Bad Sectors and Recover Readable Information

```cmd
chkdsk C: /r
```

The `/r` option locates bad sectors and attempts to recover readable information.

It also includes the functionality of `/f`.

This operation can take a long time, especially on large or damaged drives.

## 6.4 Perform an Online Scan

```cmd
chkdsk C: /scan
```

On supported NTFS volumes, `/scan` performs an online scan.

## 6.5 Display Verbose Information

```cmd
chkdsk C: /v
```

The `/v` option displays verbose output.

### Important CHKDSK Options

| Option | Description |
|---|---|
| `/f` | Fix file system errors |
| `/r` | Locate bad sectors and recover readable information |
| `/x` | Force the volume to dismount first if necessary; includes `/f` |
| `/v` | Display verbose output |
| `/scan` | Perform an online scan on supported NTFS volumes |
| `/spotfix` | Perform spot fixing on supported NTFS volumes |
| `/perf` | Use more system resources to complete a scan faster |

### Important Safety Notes

1. Run an initial check without repair options when you only want to inspect a volume.
2. Back up important data before performing repairs on a drive that may be failing.
3. `/r` can take considerable time.
4. Do not interrupt a disk repair unless necessary.
5. CHKDSK is not a substitute for recovering data from a physically failing disk.

---

# 7. DISKPART — Disk Partition Management

`diskpart` is a powerful Windows command-line utility used to manage disks, partitions, and volumes.

It provides commands for:

- Listing physical disks.
- Selecting disks.
- Listing partitions.
- Listing volumes.
- Creating partitions.
- Deleting partitions.
- Formatting volumes.
- Assigning drive letters.
- Removing drive letters.

**WARNING:** DiskPart can permanently destroy data if used incorrectly. Commands such as `clean`, `delete partition`, and `format` can cause serious data loss.

Use DiskPart only when you understand the target disk and operation.

## 7.1 Start DiskPart

```cmd
diskpart
```

You will enter the DiskPart environment.

The prompt changes to:

```text
DISKPART>
```

Exit DiskPart:

```cmd
exit
```

## 7.2 List All Physical Disks

```cmd
list disk
```

Example output:

```text
Disk ###  Status         Size
--------  -------------  -------
Disk 0    Online         512 GB
Disk 1    Online         256 GB
```

This displays detected physical disks.

## 7.3 Select a Disk

```cmd
select disk 0
```

This selects Disk 0.

Always verify the selected disk before executing any modification command.

## 7.4 Display Disk Information

```cmd
detail disk
```

This displays information about the currently selected disk.

## 7.5 List Partitions

```cmd
list partition
```

Displays partitions on the selected disk.

## 7.6 List Volumes

```cmd
list volume
```

Displays available volumes.

Example:

```text
Volume ###  Ltr  Label       Fs     Type
----------  ---  ----------  -----  ----------
Volume 0     C   Windows     NTFS   Partition
Volume 1     D   Data        NTFS   Partition
Volume 2     E   USB         exFAT  Removable
```

The actual output depends on your system.

## 7.7 Select a Volume

```cmd
select volume 2
```

This selects Volume 2.

## 7.8 Display Volume Details

```cmd
detail volume
```

Displays information about the selected volume.

---

# 8. Creating Partitions Using DiskPart

Partition creation changes disk layout and can affect existing data.

Do not perform these operations on your system disk unless you understand partitioning and have a verified backup.

## 8.1 Select a Disk

```cmd
select disk 1
```

Confirm that Disk 1 is the intended disk.

## 8.2 Create a Primary Partition

```cmd
create partition primary
```

Creates a primary partition using available unallocated space.

## 8.3 Create a Partition with a Specific Size

```cmd
create partition primary size=10240
```

The size is specified in megabytes.

Here, `10240` represents approximately 10 GB using the conventional 1024 MB per GiB calculation.

## 8.4 List Partitions

```cmd
list partition
```

Verify the newly created partition.

## 8.5 Select a Partition

```cmd
select partition 1
```

Selects Partition 1 on the selected disk.

## 8.6 Assign a Drive Letter

```cmd
assign letter=F
```

Assigns the letter F to the selected volume or partition, where supported.

**Important:** A newly created partition may need to be formatted before Windows can use it as a normal file storage volume.

---

# 9. Formatting Volumes

Formatting prepares a volume with a file system.

**WARNING:** Formatting can erase existing data. Verify the selected volume and back up important files before proceeding.

## 9.1 Format Using NTFS

Inside DiskPart, after selecting the intended volume:

```cmd
format fs=ntfs quick
```

This performs a quick NTFS format.

## 9.2 Format Using FAT32

```cmd
format fs=fat32 quick
```

FAT32 has compatibility advantages but also has limitations, including a maximum individual file size of 4 GiB.

## 9.3 Format Using exFAT

```cmd
format fs=exfat quick
```

exFAT is commonly used for removable storage and cross-platform compatibility.

### File System Comparison

| File System | Common Use | Important Characteristics |
|---|---|---|
| NTFS | Windows internal drives | Supports permissions, journaling, and large files |
| FAT32 | Older devices and compatibility | Individual files cannot exceed 4 GiB |
| exFAT | USB drives and removable storage | Supports large files and broad modern-device compatibility |

---

# 10. Assigning and Removing Drive Letters

Drive letters identify volumes in Windows.

Examples:

```text
C:
D:
E:
F:
```

## 10.1 Assign a Drive Letter

Inside DiskPart:

```cmd
select volume 2
assign letter=F
```

## 10.2 Remove a Drive Letter

```cmd
select volume 2
remove letter=F
```

Removing a drive letter does not necessarily delete the volume or its data. It removes the normal drive-letter access path.

**Important:** Avoid changing drive letters for system, boot, or application volumes without understanding the consequences.

---

# 11. CLEAN and CLEAN ALL

DiskPart provides commands that remove partition information.

These commands are extremely destructive.

## 11.1 CLEAN

```cmd
clean
```

When a disk is selected, `clean` removes the disk's partition or volume formatting information.

The disk's existing data may become inaccessible through normal Windows volume access.

## 11.2 CLEAN ALL

```cmd
clean all
```

This writes zeros to every sector of the selected disk.

It can take a long time and is destructive.

### Difference Between CLEAN and CLEAN ALL

| Command | Behavior |
|---|---|
| `clean` | Removes partition and volume formatting information |
| `clean all` | Writes zeros to every sector of the selected disk |

**Critical Warning:** Never execute these commands unless you intentionally want to erase the selected disk. Always confirm the selected disk number and its capacity.

---

# 12. DISKPART Command Reference

| Command | Purpose |
|---|---|
| `diskpart` | Start DiskPart |
| `list disk` | Display physical disks |
| `select disk` | Select a disk |
| `detail disk` | Display selected disk details |
| `list partition` | Display partitions |
| `select partition` | Select a partition |
| `list volume` | Display volumes |
| `select volume` | Select a volume |
| `detail volume` | Display selected volume details |
| `create partition primary` | Create a primary partition |
| `delete partition` | Delete the selected partition |
| `assign` | Assign a drive letter |
| `remove` | Remove a drive letter |
| `format` | Format a volume |
| `clean` | Remove partition information |
| `clean all` | Write zeros to the entire selected disk |
| `exit` | Exit DiskPart |

---

# 13. Additional Disk Information Commands

## 13.1 SYSTEMINFO

The `systeminfo` command displays detailed Windows system information, including some storage-related system details.

```cmd
systeminfo
```

This is primarily a system-information command, not a complete disk inventory utility.

## 13.2 WMIC Logical Disk Information

On Windows installations where WMIC is available:

```cmd
wmic logicaldisk get name,size,freespace,filesystem
```

This displays:

- Drive name.
- Total size.
- Free space.
- File system.

WMIC is deprecated and may not be available on newer Windows installations.

## 13.3 PowerShell Alternative

From CMD, you can run a PowerShell command:

```cmd
powershell -NoProfile -Command "Get-Volume"
```

To display physical disk information:

```cmd
powershell -NoProfile -Command "Get-Disk"
```

These commands use PowerShell rather than native CMD commands.

---

# 14. Quick Reference Table

| Command | Purpose |
|---|---|
| `vol` | Display volume label and serial number |
| `label` | Display or change volume label |
| `fsutil` | Perform advanced file system operations |
| `chkdsk` | Check file system and disk status |
| `diskpart` | Manage disks, partitions, and volumes |
| `list disk` | List physical disks in DiskPart |
| `list volume` | List volumes in DiskPart |
| `list partition` | List partitions in DiskPart |
| `assign` | Assign a drive letter |
| `remove` | Remove a drive letter |
| `format` | Format a volume |
| `clean` | Remove partition information |
| `clean all` | Write zeros to the selected disk |
| `systeminfo` | Display system information |

---

# 15. Important Differences

## 15.1 Disk vs Partition vs Volume

| Disk | Partition | Volume |
|---|---|---|
| Physical storage device | Division of a disk | Usable storage area |
| Example: SSD | Example: Partition 1 | Example: C: |
| Contains partitions | Can contain or support a volume | Stores files using a file system |

## 15.2 CHKDSK vs FORMAT

| CHKDSK | FORMAT |
|---|---|
| Checks a volume's file system | Prepares a volume with a file system |
| Can repair certain file system errors | Can erase existing data |
| Does not normally reformat the volume | Creates a new file system structure |

## 15.3 DISKPART vs DISK MANAGEMENT

| DiskPart | Disk Management |
|---|---|
| Command-line utility | Graphical Windows utility |
| Supports scripting | Uses a graphical interface |
| Offers advanced disk operations | Provides visual disk management |
| Requires careful command execution | Provides visual confirmation of disk layout |

---

# 16. Important Safety Guidelines

1. Always identify the correct disk before using DiskPart.
2. Verify disk number, size, and status.
3. Back up important data before modifying partitions.
4. Never use `clean` or `clean all` casually.
5. Never format a volume without verifying its identity.
6. Do not delete system or recovery partitions without understanding their purpose.
7. Use CHKDSK carefully on drives showing signs of physical failure.
8. Do not assume that removing a drive letter deletes a volume.
9. Avoid modifying boot or system partitions unnecessarily.
10. Open CMD as Administrator only when the operation requires it.

---

# 17. Key Takeaways

After studying this lesson, you should understand:

- Disk, partition, volume, and file system concepts.
- How Windows drive letters work.
- How to inspect volume information using `vol`.
- How to change volume labels using `label`.
- How to inspect file system information using `fsutil`.
- How to check file system errors using `chkdsk`.
- How to inspect disks and partitions using DiskPart.
- How to create partitions.
- How to format volumes.
- How to assign and remove drive letters.
- The difference between `clean` and `clean all`.
- How to inspect storage information using PowerShell from CMD.

---

# 18. Official Microsoft Documentation

- [Windows Commands](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [CHKDSK](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/chkdsk)
- [DISKPART](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/diskpart)
- [FSUTIL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/fsutil)
- [FORMAT](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/format)
- [VOL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/vol)
- [LABEL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/label)
- [SYSTEMINFO](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/systeminfo)
- [ROBOCOPY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy)

---

**End of Lesson 04 — Disk and Drive Management in Windows CMD**
