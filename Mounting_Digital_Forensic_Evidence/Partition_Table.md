# **Know the Partition Table: Unlocking Storage Structures**

---

## **Introduction**

Understanding the structure of digital storage media is a fundamental skill in the world of digital forensics. The "Know the Partition Table" directory is your gateway to mastering this crucial aspect of forensic investigation.

In this directory, we delve deep into the concept of partition tables and their significance. A partition table is like a roadmap of a storage device, guiding investigators to the exact location of data within. By grasping the nuances of partition tables, you gain the power to identify, select, and access the partitions that hold the key to the digital evidence you're seeking.

### Why Partition Tables Matter

Partition tables contain essential information about how a storage device is organized. They detail the location, size, and attributes of individual partitions, which are distinct sections of the storage medium. In the world of digital forensics, a sound understanding of partition tables is indispensable because it allows you to pinpoint the precise area of interest, be it a particular partition on a hard drive, USB flash drive, or other storage media.

### Using `mmls` to Display Partition Table

In this section, we will explore the usage of the **`mmls`** command, a powerful tool for digital forensics, to display the partition table of storage devices. **`mmls`** provides a quick and effective way to inspect and understand the structure of storage media, helping investigators identify and access the partitions crucial to their investigations. This command is an invaluable asset in the process of "Knowing the Partition Table," allowing forensic analysts to gain insights into the organization of storage media.

**Command:**
- **`mmls <path_of_container>`**




Here is something very important to notice, and it is that the `mmls` command will give us the sector of each partition. This is the number that we can locate at the start column. A sector is the smallest addressable unit on a storage device, such as a hard drive or SSD. It typically consists of 512 bytes of data, although there are variations (e.g., 4096-byte sectors) on some modern storage devices. The sector number represents the physical location on the storage medium where data is stored.

### Example:

- Run `mmls <container>`:
  
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/a52b1e12-5756-428d-91f6-ef90893ba135)
   - Here we can see that we have a privary table, 2 unallocated spaces and 2 partitions with NTFS / exFAT.
   - The sector of the first partition is 2048 and the sector of the second is 206848
