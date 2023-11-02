# **Mounting the File System: Accessing Data for Analysis.**

---

## **Introduction**

Once the digital forensic investigator has identified the file system within an evidence container, the next critical step is to mount that file system. Mounting allows you to access the data stored within the file system as if it were a standard filesystem, making it available for analysis and investigation.

In the "Mounting the File System" directory, we will explore the procedures, tools, and techniques necessary to successfully mount file systems of various types. Whether you're dealing with NTFS, ext4, FAT32, or other filesystems, this directory will guide you through the process of mounting with precision.

### Why Mounting Matters

Mounting a file system is a pivotal moment in a digital forensic investigation. It enables you to view, search, and analyze the data contained within the file system, uncovering valuable insights and potential evidence. Understanding how to mount file systems is an essential skill for any digital forensic analyst.

**Sector Offset:**

The sector offset is a way to address a specific sector within a storage medium relative to a starting point, often used for forensic analysis.  It is calculated as the sector number multiplied by the sector size (typically 512 bytes). The result is the byte offset from the beginning of the storage device.

**Why Identify the Sector Offset?**

File systems within digital evidence containers may not always start at the very beginning of the container. Instead, they are often located at a certain sector offset within the container. Therefore, knowing the sector offset is essential for targeting the correct location of the file system.

**How to Determine the Sector Offset:**

1. **Start Sector:** Begin by using a tool like **`mmls`** to identify the start sector of the partition or file system you wish to analyze. This start sector represents the sector number at which the file system begins.
2. **Calculating Sector Offset:** To obtain the sector offset, simply multiply the start sector number by the sector size (usually 512 bytes).
    
    For example, if **`mmls`** provides a start sector number of 1000, the sector offset would be 1000 * 512 = 512,000.
    

### Mounting Commands for Different File Systems

Depending on the file system used in the digital evidence you're examining, you'll need to use specific commands. Below, you'll find a list of commands tailored to different file system types. Choose the one that matches your case:

- **NTFS:** `sudo mount -o ro,noexec,loop,offset=<offset>,show_sys_files,streams_interface=windows <img> <dest>`
- **HFS, HFS+:** `sudo mount -o ro,offset=<offset>,sizelimit=<partsize> <img> <dest>`
- **EXT3, EXT4:** `sudo mount -o ro,offset=<offset>,noload <img> <dest>`
- **XFS:** `sudo mount -o ro,offset=<offset>,norecovery <img> <dest>`
- **Others:** `sudo mount -o ro,offset=<offset>,noexe,loop <img> <dest>`

### Example:

- Create one directory for each partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/6f5e8e42-d99b-421a-952d-affe956175d4)

- Mount the first partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/e848a436-f82e-4ba4-9eec-25aa9382bcaf)
   - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/82e73a1d-49f1-4ff1-ac98-49d4a1f2bdcd)


- Mount the second partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/813b7396-378d-462e-a21a-0ed0c67485ce)
  - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/ae6819d0-6dab-4e48-8b80-d4d73df8aad3)
